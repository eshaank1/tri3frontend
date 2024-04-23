---
permalink: /house
---

# Northeastern US House Price Predictor
### Eshaan Kumar

This is a tool to predict the price of a northeastern US home based on various details of the home including:
- Acre Lot
- Bedrooms
- Bathrooms

<html lang="en">

    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>House Price Prediction</title>


    <h1>Northeastern US House Price Prediction</h1>

    <label for="acre_lot">Acre Lot:</label>
    <input type="number" id="acre_lot">
    <span class="info-icon" title="Suggested range: 1 - 1800">&#9432;</span><br><br>


    <label for="bedrooms">Bedrooms:</label>
    <input type="number" id="bedrooms">
    <span class="info-icon" title="Suggested range: 1 - 11">&#9432;</span><br><br>


    <label for="bathrooms">Bathrooms:</label>
    <input type="number" id="bathrooms">
    <span class="info-icon" title="Suggested range: 1 - 15">&#9432;</span><br><br>


    <button onclick="predictPrice()">Predict Price</button><br><br>
    <button onclick="saveSettings()">Save Settings</button><br><br>

    <div id="predict"></div>
    <p id="result"></p>
<style>
    .info-icon {
        margin-left: 5px;
        cursor: pointer;
        font-size: 18px;
    }

    .info-icon:hover {
        color: blue;
    }
</style>

<script>
    function predictPrice() {
        const acreLot = document.getElementById("acre_lot").value;
        const bedrooms = document.getElementById("bedrooms").value;
        const bathrooms = document.getElementById("bathrooms").value;

        const acreLotInRange = acreLot >= 1 && acreLot <= 1800;
        const bedroomsInRange = bedrooms >= 1 && bedrooms <= 11;
        const bathroomsInRange = bathrooms >= 1 && bathrooms <= 15;

        if (!acreLotInRange || !bedroomsInRange || !bathroomsInRange) {
            document.getElementById("result").innerText = "Please enter values within the suggested range.";
            return
        }

        const requestData = {
            "acre_lot": acreLot,
            "bedrooms": bedrooms,
            "bathrooms": bathrooms
        };
        console.log(JSON.stringify(requestData))
        fetch("http://127.0.0.1:8059/api/houseprice/predict", {
            method: "POST",
            headers: {
                "Content-Type": "application/json",
            },
            body: JSON.stringify(requestData),
        })
        .then(response => response.json())
        .then(data => {
            const predictedPrice = parseFloat(data.predicted_price).toLocaleString(); // Add parseFloat() to ensure correct conversion to number before formatting
            document.getElementById("result").innerText = "Predicted Price: $" + predictedPrice;
        })
        .catch(error => {
            console.error("Error:", error);
            document.getElementById("result").innerText = "An error occurred. Please try again.";
        });
    }

    function saveSettings() {
        const acreLot = document.getElementById("acre_lot").value;
        const bedrooms = document.getElementById("bedrooms").value;
        const bathrooms = document.getElementById("bathrooms").value;
        const requestData = {
            "acre_lot": acreLot,
            "bedrooms": bedrooms,
            "bathrooms": bathrooms
        };
        fetch("http://127.0.0.1:8059/api/houseprice/settings", {
            method: "POST", // Change method to POST
            headers: {
                "Content-Type": "application/json",
            },
            body: JSON.stringify(requestData),
        })
        .then(response => {
            if (response.ok) {
                alert("Settings saved successfully!");
            } else {
                alert("Failed to save settings. Please try again.");
            }
        })
        .catch(error => {
            console.error("Error:", error);
            alert("An error occurred. Please try again.");
        });
    }

    

    // Load settings when the page loads
    window.addEventListener('load', loadSettings);

</script>


    

</html>
