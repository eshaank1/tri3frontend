---
permalink: /ninaad-titanic
---

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Titanic Survival Prediction</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            padding: 20px;
        }
        label, input, button {
            display: block;
            margin: 10px 0;
        }
        input, button {
            padding: 10px;
        }
        button {
            cursor: pointer;
            background-color: #007bff;
            color: white;
            border: none;
            border-radius: 5px;
        }
        button:hover {
            background-color: #0056b3;
        }
        #predictionResult {
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <h2>Titanic Survival Prediction</h2>
    <form id="predictionForm">
        <label for="pclass">Passenger Class (1, 2, 3):</label>
        <input type="number" id="pclass" name="pclass" min="1" max="3" required>
        <label for="sex">Sex (male or female):</label>
        <input type="text" id="sex" name="sex" required>
        <label for="age">Age:</label>
        <input type="number" id="age" name="age" required>
        <label for="sibsp">Number of Siblings/Spouses Aboard:</label>
        <input type="number" id="sibsp" name="sibsp" required>
        <label for="parch">Number of Parents/Children Aboard:</label>
        <input type="number" id="parch" name="parch" required>
        <label for="fare">Fare:</label>
        <input type="number" step="0.01" id="fare" name="fare" required>
        <label for="embarked">Embarked (C, Q, S):</label>
        <input type="text" id="embarked" name="embarked" required>
        <button type="button" onclick="submitForm()">Predict Survival</button>
    </form>
    <div id="predictionResult"></div>
    <script>
        function submitForm() {
            const form = document.getElementById('predictionForm');
            const formData = new FormData(form);

            // Convert form data to a JSON object
            const jsonObject = {};
            formData.forEach((value, key) => { jsonObject[key] = value; });

            // Specify the API URL including the port
            const apiUrl = 'http://127.0.0.1:8057/api/titanic/predict';

            fetch(apiUrl, {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                },
                body: JSON.stringify(jsonObject),
            })
            .then(response => response.json())
            .then(data => {
                document.getElementById('predictionResult').innerHTML = `DT Probability: ${data['DT Probability']}, LogReg Probability: ${data['LogReg Probability']}`;
            })
            .catch((error) => {
                console.error('Error:', error);
                document.getElementById('predictionResult').innerHTML = 'Error making prediction.';
            });
        }
    </script>
</body>
</html>
