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
        // Create constants for each of the user input values
        const acreLot = parseInt(document.getElementById("acre_lot").value);
        const bedrooms = parseInt(document.getElementById("bedrooms").value);
        const bathrooms = parseInt(document.getElementById("bathrooms").value);

        // Create list for the 3 inputs
        const inputs = [acreLot, bedrooms, bathrooms];

        // Create a list with nested dictionaries for each variable along with its ranges
        const inputFields = [
            { id: "acre_lot", range: { min: 1, max: 1800 } },
            { id: "bedrooms", range: { min: 1, max: 11 } },
            { id: "bathrooms", range: { min: 1, max: 15 } }
        ];

        // Iterate through for loop along with conditional if statement to ensure inputs are within range
        for (let i = 0; i < inputs.length; i++) {
            const value = inputs[i];
            const range = inputFields[i].range; // Get the range from inputFields array
            if (value < range.min || value > range.max) {
                document.getElementById("result").innerText = "Please enter values within the suggested range.";
                return;
            }
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

    function loadSettings() {
        fetch("http://127.0.0.1:8059/api/houseprice/settings", {
            method: "GET",
        })
        .then(response => response.json())
        .then(data => {
            document.getElementById("acre_lot").value = data.acre_lot || '';
            document.getElementById("bedrooms").value = data.bedrooms || '';
            document.getElementById("bathrooms").value = data.bathrooms || '';
        })
        .catch(error => {
            console.error("Error:", error);
            alert("An error occurred while loading settings. Please try again.");
        });
    }

    // Load settings when the page loads
    window.addEventListener('load', loadSettings);

</script>
</html>
