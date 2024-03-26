---
toc: true
comments: false
layout: post
title: Diamond ML
type: hacks
courses: { compsci: {week: 28} }
---

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Diamond Price Prediction</title>
<script>
async function predictPrice() {
    // Get the input values from the form
    const carat = document.getElementById('carat').value;
    const cut = document.getElementById('cut').value;
    const color = document.getElementById('color').value;
    const clarity = document.getElementById('clarity').value;
    const depth = document.getElementById('depth').value;
    const table = document.getElementById('table').value;
    const x = document.getElementById('x').value;
    const y = document.getElementById('y').value;
    const z = document.getElementById('z').value;

    // Prepare the data in JSON format
    const data = {
        carat: parseFloat(carat),
        cut: cut,
        color: color,
        clarity: clarity,
        depth: parseFloat(depth),
        table: parseFloat(table),
        x: parseFloat(x),
        y: parseFloat(y),
        z: parseFloat(z)
    };

    // Make a POST request to the server
    const response = await fetch('http://127.0.0.1:8032/api/diamond/predict', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json'
        },
        body: JSON.stringify(data)
    });

    // Parse the JSON response
    const result = await response.json();

    // Display the result
    if (response.ok) {
        document.getElementById('result').textContent = 'Predicted Price: ' + result.prediction;
    } else {
        document.getElementById('result').textContent = 'Error: ' + result.error;
    }
}
</script>
</head>
<body>
<h1>Diamond Price Predictor</h1>
<form onsubmit="event.preventDefault(); predictPrice();">
    <label for="carat">Carat:</label>
    <input type="number" id="carat" step="0.01" required><br>

    <label for="cut">Cut:</label>
    <select id="cut" required>
        <option value="Ideal">Ideal</option>
        <option value="Premium">Premium</option>
        <option value="Good">Good</option>
        <option value="Fair">Fair</option>
        <option value="Poor">Poor</option>
    </select><br>

    <label for="color">Color:</label>
    <select id="color" required>
        <option value="D">D</option>
        <option value="E">E</option>
        <option value="F">F</option>
        <!-- Add other options as needed -->
    </select><br>

    <label for="clarity">Clarity:</label>
    <select id="clarity" required>
        <option value="IF">IF</option>
        <option value="VVS1">VVS1</option>
        <option value="VVS2">VVS2</option>
        <!-- Add other options as needed -->
    </select><br>

    <label for="depth">Depth:</label>
    <input type="number" id="depth" step="0.1" required><br>

    <label for="table">Table:</label>
    <input type="number" id="table" step="0.1" required><br>

    <label for="x">Length (x):</label>
    <input type="number" id="x" step="0.01" required><br>

    <label for="y">Width (y):</label>
    <input type="number" id="y" step="0.01" required><br>

    <label for="z">Depth (z):</label>
    <input type="number" id="z" step="0.01" required><br>

    <button type="submit">Predict Price</button>
</form>

<div id="result"></div>

</body>
</html>
