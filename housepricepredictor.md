---
toc: false
comments: false
layout: post
title: House Price Predictor
type: hacks
courses: { compsci: {week: 28} }
---

# House Price Predictor
### Eshaan Kumar

This is a tool to predict the price of a home based on various details of the home including:
- Location
- Square Footage
- Bedrooms
- Bathrooms

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>House Price Prediction</title>
</head>
<body>
    <h1>House Price Prediction</h1>

    // The following labels create input boxes for the user
    <label for="location">Location:</label>
    <input type="text" id="location"><br><br>

    <label for="square_footage">Square Footage:</label>
    <input type="number" id="square_footage"><br><br>

    <label for="bedrooms">Bedrooms:</label>
    <input type="number" id="bedrooms"><br><br>

    <label for="bathrooms">Bathrooms:</label>
    <input type="number" id="bathrooms"><br><br>

    // Button for user to click and recieve a prediction
    <button onclick="predictPrice()">Predict Price</button><br><br>

    <div id="result"></div>

    
</body>
</html>
