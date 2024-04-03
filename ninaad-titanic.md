---
permalink: /ninaad-titanic
---

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Titanic Survival Prediction</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
            padding: 20px;
        }

        label, input {
            margin-bottom: 10px;
            display: block;
        }

        button {
            margin-top: 20px;
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

            fetch('http://127.0.0.1:8058/api/titanic/predict', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                },
                body: JSON.stringify([formData]),
            })
            .then(response => response.json())
            .then(data => {
                document.getElementById('predictionResult').innerHTML = `
                    <p>Decision Tree Classifier Survival Probability: ${data['DecisionTreeClassifier Survival Probability']}</p>
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

