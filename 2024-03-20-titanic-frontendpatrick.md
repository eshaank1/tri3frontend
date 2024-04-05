---
permalink: /patricktitanic
---
<html lang="en">
<head> 
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Titanic Survival Prediction</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            background-color: #f0f0f0; /* light Grey */
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }
        .container {
            background-color: #ffffff; /* white */
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            width: 300px;
        }
        h2 {
            text-align: center;
            color: #333333; /* contrasting text color */
        }
        form {
            display: flex;
            flex-direction: column;
        }
        label {
            margin-top: 10px;
            color: #333333; /* contrasting text color */
        }
        input, select, button {
            padding: 10px;
            margin-top: 5px;
            border: 1px solid #dddddd; /* grey border */
            border-radius: 4px;
            /* contrasting text color */
            color: #333333; /* contrasting text color*/
        }
        input::placeholder {
            color: #aaaaaa; 
            opacity: 1; 
        }
        button {
            background-color: #008080; /* teal button */
            color: white;
            margin-top: 20px;
            border: none;
            cursor: pointer;
        }
        button:hover {
            background-color: #005454; /* contrasting teal */
        }
        #predictionResult {
            margin-top: 20px;
            text-align: center;
            padding: 10px;
            background-color: #dddddd; /* dark grey */
            border-radius: 4px;
            display: none; /* initially hide */
            color: #333333; /* Dark gray text */
        }
    </style> 
</head>
<body>
    <div class="container">
        <h2>Titanic Survival Predictor</h2>
        <form id="predictionForm">
            <label for="pclass">Class:</label>
            <select id="pclass">
                <option value="1">1st Class</option>
                <option value="2" selected>2nd Class</option>
                <option value="3">3rd Class</option>
            </select>
            <label for="sex">Sex:</label>
            <select id="sex">
                <option value="1">Male</option>
                <option value="0">Female</option>
            </select>
            <label for="age">Age:</label>
            <input type="number" id="age" placeholder="Age" required>
            <label for="sibsp">Siblings/Spouses Aboard:</label>
            <input type="number" id="sibsp" placeholder="Siblings/Spouses" required>
            <label for="parch">Parents/Children Aboard:</label>
            <input type="number" id="parch" placeholder="Parents/Children" required>
            <label for="fare">Fare:</label>
            <input type="number" step="0.01" id="fare" placeholder="Ticket Fare" required>
            <label for="alone">Traveling Alone:</label>
            <input type="checkbox" id="alone">
            <label for="embarked">Embarked From:</label>
            <select id="embarked">
                <option value="S">Southampton</option>
                <option value="C">Cherbourg</option>
                <option value="Q">Queenstown</option>
            </select>
            <button type="submit">Predict Survival</button>
        </form>
        <div id="predictionResult"></div>
    </div>
    <script> // js that handles int w api and the form submisson
        document.getElementById('predictionForm').onsubmit = async function(e) {
            e.preventDefault();
            const formData = { // extract form data
                pclass: document.getElementById('pclass').value,
                sex: document.getElementById('sex').value,
                age: document.getElementById('age').value,
                sibsp: document.getElementById('sibsp').value,
                parch: document.getElementById('parch').value,
                fare: document.getElementById('fare').value,
                alone: document.getElementById('alone').checked ? 1 : 0,
                embarked: document.getElementById('embarked').value
            }; // send data to api to get prediction
            const response = await fetch('http://127.0.0.1:8086/api/titanic/predict', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                },
                body: JSON.stringify(formData),
            });
            const result = await response.json(); // get prediction from api
            const resultDiv = document.getElementById('predictionResult');// display prediction
            resultDiv.style.display = 'block'; // Show the result
            resultDiv.innerText = 
                // `Survival Probability (Decision Tree): ${result['DT Probability']}\n` +
                `Survival Prediction: ${result['LogReg Probability']}`;
        };
    </script>
</body>
</html>
