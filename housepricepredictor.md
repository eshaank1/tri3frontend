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
- Acre Lot
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

    <label for="acre_lot">Acre Lot:</label>
    <input type="number" id="acre_lot"><br><br>

    <label for="bedrooms">Bedrooms:</label>
    <input type="number" id="bedrooms"><br><br>

    <label for="bathrooms">Bathrooms:</label>
    <input type="number" id="bathrooms"><br><br>

    <button onclick="predictPrice()">Predict Price</button><br><br>

    <div id="predict"></div>

<script>
    function predictPrice() {
        const acreLot = document.getElementById("acre_lot").value;
        const bedrooms = document.getElementById("bedrooms").value;
        const bathrooms = document.getElementById("bathrooms").value;

        const requestData = {
            "sqft": acre_lot,
            "bedrooms": bedrooms,
            "bathrooms": bathrooms
        };

        fetch("http://127.0.0.1:8086/api/houseprice/", {
            method: "POST",
            headers: {
                "Content-Type": "application/json",
            },
            body: JSON.stringify(requestData),
        })
        .then(response => response.json())
        .then(data => {
            document.getElementById("result").innerText = "Predicted Price: $" + data.predicted_price;
        })
        .catch(error => {
            console.error("Error:", error);
            document.getElementById("result").innerText = "An error occurred. Please try again.";
        });
    }
</script>


    
</body>
</html>
