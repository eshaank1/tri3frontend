---
permalink: /mpg
---

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MPG Prediction</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #F4F4F4;
            margin: 0;
            padding: 20px;
            color: #333;
        }
        h1 {
            color: #0056B3;
        }
        form {
            background: #fff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        label {
            margin-top: 10px;
            display: inline-block;
            color: #333;
        }
        input, select {
            margin-bottom: 10px;
            border: 1px solid #ddd;
            border-radius: 4px;
            padding: 8px;
            width: calc(100% - 22px);
        }
        button {
            background-color: #4CAF50;
            color: white;
            padding: 10px 20px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }
        button:hover {
            background-color: #45A049;
        }
        #result {
            margin-top: 20px;
            padding: 20px;
            background-color: #E2E2E2;
            border-radius: 4px;
            color: #333;
        }
        .legend {
            margin-top: 20px;
            background: #fff;
            padding: 10px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            color: #333;
        }
        .legend h2 {
            color: #0056B3;
        }
        .legend p {
            font-size: 14px;
            line-height: 1.6;
        }
    </style>
</head>
<body>
    <h1>MPG Predictor</h1>
    <form onsubmit="event.preventDefault(); predictMPG();">
        <label for="cylinders">Cylinders:</label>
        <input type="number" id="cylinders" required><br>
        
        <label for="displacement">Displacement:</label>
        <input type="number" id="displacement" required><br>
        
        <label for="horsepower">Horsepower:</label>
        <input type="number" id="horsepower" required><br>
        
        <label for="weight">Weight:</label>
        <input type="number" id="weight" required><br>
        
        <label for="acceleration">Acceleration:</label>
        <input type="number" id="acceleration" required><br>
        
        <label for="model_year">Model Year:</label>
        <input type="number" id="model_year" required><br>
        
        <label for="origin">Origin:</label>
        <select id="origin" required>
            <option value="1">USA</option>
            <option value="2">Europe</option>
            <option value="3">Japan</option>
        </select><br>
        
        <button type="submit">Predict MPG</button>
    </form>
    <div id="result"></div>
    <div class="legend">
        <h2>Parameter Legend</h2>
        <p><strong>Cylinders:</strong> Number of engine cylinders. More cylinders usually mean more power but less fuel efficiency.</p>
        <p><strong>Displacement:</strong> Engine displacement in cubic centimeters. Larger engines can produce more power.</p>
        <p><strong>Horsepower:</strong> Engine power output in horsepower. Higher horsepower indicates a more powerful engine.</p>
        <p><strong>Weight:</strong> Vehicle weight in pounds. Heavier vehicles generally consume more fuel.</p>
        <p><strong>Acceleration:</strong> Time in seconds to accelerate from 0 to 60 mph. Indicates vehicle's ability to gain speed.</p>
        <p><strong>Model Year:</strong> The year the vehicle model was released. Newer models may have better fuel efficiency.</p>
        <p><strong>Origin:</strong> The country where the vehicle was manufactured. This can influence the design and fuel efficiency.</p>
    </div>
    <script>
    async function predictMPG() {
        const data = {
            cylinders: parseInt(document.getElementById('cylinders').value),
            displacement: parseFloat(document.getElementById('displacement').value),
            horsepower: parseFloat(document.getElementById('horsepower').value),
            weight: parseFloat(document.getElementById('weight').value),
            acceleration: parseFloat(document.getElementById('acceleration').value),
            model_year: parseInt(document.getElementById('model_year').value),
            origin: document.getElementById('origin').value
        };

        try {
            const response = await fetch('http://127.0.0.1:8058/api/mpg/predict', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify(data)
            });

            const result = await response.json();
            if (response.ok) {
                document.getElementById('result').textContent = 'Predicted MPG: ' + result.prediction;
            } else {
                document.getElementById('result').textContent = 'Error: ' + result.error;
            }
        } catch (error) {
            console.error('Error:', error);
            document.getElementById('result').textContent = 'Failed to fetch prediction';
        }
    }
    </script>
</body>
</html>
