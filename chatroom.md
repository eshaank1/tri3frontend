---
permalink: /chat
---
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Chatroom</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #232122;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background-image: url('{{site.baseurl}}/images/logincar.gif'); /* Add your GIF URL here */
            background-size: cover; /* Ensure the background covers the full viewport */
            background-position: center; /* Center the background image */
            background-repeat: no-repeat; /* Prevent the background image from repeating */
        }
        .chatroom {
            width: 600px;
            height: 600px;
            background-color: #232122;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            overflow: hidden;
        }
        .chatroom-header {
            background-color: #C13A7F;
            color: #FFF;
            text-align: center;
            padding: 10px;
            border-bottom: 1px solid #C13A7F;
        }
        .chatroom-messages {
            max-height: 460px;
            min-height: 460px;
            padding: 8px;
            overflow-y: auto;
            background-color: #232122; /* Adjust this for better visibility against background */
        }
        .chatroom-messages div {
            background-color: #C13A7F;
            border-radius: 5px;
            margin: 5px 0;
            padding: 5px;
            word-wrap: break-word;
            cursor: pointer;
        }
        .chatroom-input {
            padding: 10px;
            display: flex;
            border-top: 1px solid #FFFFFF;
        }
        input[type="text"] {
            flex: 1;
            padding: 10px;
            border: none;
            border-radius: 5px;
            background-color: #C13A7F;
            color: #FFFFFF;
        }
        button {
            background-color: #C13A7F;
            color: #FFFFFF;
            border: none;
            border-radius: 5px;
            padding: 10px 20px;
            cursor: pointer;
            margin-left: 10px;
        }
    </style>
</head>
<body>
    <div class="chatroom">
        <div class="chatroom-header">
            <h1>Chatroom</h1>
        </div>
        <div class="chatroom-messages" id="chatroom-messages">
            <!-- Messages will be displayed here -->
        </div>
        <div class="chatroom-input">
            <input type="text" id="message" placeholder="Type your message here..." onkeypress="handleKeyPress(event)">
            <button id="send" onclick="sendMessage()">Send</button>
            <button id="toggleModeButton" onclick="toggleMode()">Toggle Mode</button>
        </div>
    </div>
    <script>
        const chatBox = document.getElementById("chatroom-messages");
        const messageInput = document.getElementById("message");
        const backendUrl = "http://127.0.0.1:8059"; // Replace with your backend URL
        let currentMessageId = null; // Track the current message being edited

function sendMessage() {
    const message = messageInput.value.trim();
    if (message !== '') {
        // Determine the endpoint and method based on whether there's a currentMessageId
        const apiEndpoint = currentMessageId ? `${backendUrl}/api/chat/edit` : `${backendUrl}/api/chat/create`;
        const methodType = currentMessageId ? "PUT" : "POST";
        const payload = currentMessageId ? { message_id: currentMessageId, message: message } : { message: message };

        fetch(apiEndpoint, {
            method: methodType,
            headers: {
                "Content-Type": "application/json",
            },
            body: JSON.stringify(payload),
        })
        .then(response => response.json())
        .then(data => {
            if (data.error) {
                throw new Error(data.error);
            }
            displayChat(); // Refresh chat messages
            messageInput.value = ''; // Clear input field
            currentMessageId = null; // Reset the current message ID
        })
        .catch(error => {
            console.error("API error:", error);
        });
    }
}
function editMessage(messageId) {
    currentMessageId = messageId; // Set the current message ID
    const messageDiv = document.getElementById(`message-${messageId}`);
    const messageTextWithTimestamp = messageDiv.textContent;
    // Assuming the timestamp format is [HH:MM] message, we remove the timestamp part
    const messageText = messageTextWithTimestamp.substring(messageTextWithTimestamp.indexOf(']') + 2);
    messageInput.value = messageText; // Set the message text without the timestamp
    messageInput.focus(); // Focus the input field
}


function displayChat() {
    fetch(backendUrl + '/api/chat/read', {
        method: "GET",
    })
    .then((response) => {
        if (response.ok) {
            return response.json(); // Parse response as JSON
        } else {
            throw new Error('Failed to retrieve chat messages'); // Handle error if necessary
        }
    })
    .then((data) => {
        chatBox.innerHTML = ""; // Clear current messages
        data.forEach((item) => {
            const messageElement = document.createElement("div");
            const formattedTimestamp = new Date(item.timestamp).toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' });
            messageElement.textContent = `[${formattedTimestamp}] ${item.message}`;
            messageElement.id = `message-${item.id}`;
            messageElement.onclick = () => editMessage(item.id);
            chatBox.appendChild(messageElement);
        });
    })
    .catch((error) => {
        console.error("Failed to retrieve chat messages:", error);
    });
}


        function handleKeyPress(event) {
            if (event.key === "Enter") {
                event.preventDefault();
                sendMessage();
            }
        }

        displayChat(); // Initial chat load
        setInterval(displayChat, 5000); // Update chat every 5 seconds
    </script>
</body>
</html>
