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
        font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        background-color: #f4f4f4;
        margin: 0;
        padding: 20px;
        color: #333;
    }

    h1 {
        color: #0056b3;
    }

    form {
        background-color: #fff;
        max-width: 600px;
        margin: 20px auto;
        padding: 20px;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        border-radius: 8px;
    }

    label {
        margin-top: 10px;
        margin-bottom: 5px;
        font-weight: bold;
        display: block;
    }

    input[type="number"],
    input[type="text"] {
        width: 100%;
        padding: 8px;
        margin-bottom: 20px;
        border: 1px solid #ddd;
        border-radius: 4px;
        box-sizing: border-box;
    }

    button {
        background-color: #0056b3;
        color: #ffffff;
        border: none;
        padding: 10px 20px;
        text-align: center;
        text-decoration: none;
        display: inline-block;
        font-size: 16px;
        margin: 4px 2px;
        cursor: pointer;
        border-radius: 4px;
        transition: background-color 0.3s ease;
    }

    button:hover {
        background-color: #004494;
    }

    #predictionResult {
        max-width: 600px;
        margin: 20px auto;
        padding: 20px;
        background-color: #964B00;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        border-radius: 8px;
    }

    #predictionResult p {
        font-weight: bold;
        color: #333;
    }
</style>

</head>
<body>
    <h1>Titanic Survival Prediction</h1>
    <form id="predictionForm">
        <label for="pclass">Passenger Class:</label>
        <input type="number" id="pclass" name="pclass" required><br>

        <label for="sex">Sex (0 for female, 1 for male):</label>
        <input type="number" id="sex" name="sex" required><br>

        <label for="age">Age:</label>
        <input type="number" id="age" name="age" required><br>

        <label for="sibsp">Siblings/Spouses Aboard:</label>
        <input type="number" id="sibsp" name="sibsp" required><br>

        <label for="parch">Parents/Children Aboard:</label>
        <input type="number" id="parch" name="parch" required><br>

        <label for="fare">Ticket Fare:</label>
        <input type="number" step="any" id="fare" name="fare" required><br>

        <label for="embarked">Embarked (C = Cherbourg; Q = Queenstown; S = Southampton):</label>
        <input type="text" id="embarked" name="embarked" required><br>

        <label for="alone">Alone (0 for No, 1 for Yes):</label>
        <input type="number" id="alone" name="alone" required><br>

        <button type="submit">Predict Survival</button>
    </form>
    <div id="predictionResult"></div>
    <script>
        document.getElementById('predictionForm').addEventListener('submit', function(e) {
            e.preventDefault();

            const formData = {
                pclass: document.getElementById('pclass').value,
                sex: document.getElementById('sex').value,
                age: document.getElementById('age').value,
                sibsp: document.getElementById('sibsp').value,
                parch: document.getElementById('parch').value,
                fare: document.getElementById('fare').value,
                embarked: document.getElementById('embarked').value.toUpperCase(),
                alone: document.getElementById('alone').value
            };

            fetch('http://127.0.0.1:8059/api/titanic/predict', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                },
                body: JSON.stringify([formData]),
            })
            .then(response => response.json())
            .then(data => {
                document.getElementById('predictionResult').innerHTML = `
                    <p>Logistic Regression Survival Probability: ${data['LogisticRegression Survival Probability']}</p>
                `;
            })
            .catch((error) => {
                console.error('Error:', error);
            });
        });
    </script>
</body>
</html>

