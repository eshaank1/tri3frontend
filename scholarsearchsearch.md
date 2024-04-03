---
layout: default
title: Search
---
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="/ScholarSearch/assets/common/css/style.css">
    <link rel="stylesheet" href="/ScholarSearch/assets/pages/search/css/style.css">
    <title>College Search</title>
    <style>
        .container {
            max-width: 800px;
            margin: 20px auto;
            padding: 20px;
            background-color: white;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.3);
            border-radius: 10px;
            overflow: hidden;
        }
        /* Search form */
        #searchForm {
            display: flex;
            justify-content: center;
            align-items: center;
            margin-bottom: 20px;
        }
        #searchInput {
            flex: 1;
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
        #searchButton:hover {
            background-color: #0056b3;
        }
        /* Search results */
        #searchResults {
            background-color: white;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.3);
            padding: 20px;
        }
        .searchResult {
            margin-bottom: 10px;
            padding: 10px;
            border-bottom: 1px solid #ccc;
        }
        .searchResult:last-child {
            border-bottom: none;
        }
        .searchResult h3 {
            margin: 0;
            color: #007bff;
        }
        .searchResult p {
            margin-top: 5px;
            color: #666;
        }
        .flex-container {
            display: flex;
            align-items: left;
            justify-content: space-between;
        }
        .button {
            border-radius: 10px;
            background-color: light gray;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            padding-left: 10px;
            padding-right: 10px;
            border: 1px solid #000;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>College Search</h1>
        <form id="searchForm">
            <label for="searchInput">Search by College Name:&nbsp; </label>
            <input type="text" id="searchInput" name="searchInput" placeholder="Enter college name">
        </form>
        <div id="searchResults">
        </div>
    </div>
    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const searchForm = document.getElementById('searchForm');
            const searchInput = document.getElementById('searchInput');
            const searchResults = document.getElementById('searchResults');

            searchForm.addEventListener('submit', function(event) {
                event.preventDefault(); // Prevent the form from submitting normally
                performSearch(searchInput.value);
            });

            function performSearch(query) {
                // Placeholder for search logic
                searchResults.innerHTML = ''; // Clear previous results

                if (query.trim() === '') {
                    searchResults.innerHTML = '<p>Please enter a search term.</p>';
                    return;
                }

                // Simulating a search result
                const resultDiv = document.createElement('div');
                resultDiv.classList.add('searchResult');
                resultDiv.innerHTML = `
                    <h3>Search Result for "${query}"</h3>
                    <p>This is a simulated search result. Replace this logic with actual search functionality.</p>
                `;

                searchResults.appendChild(resultDiv);
            }
        });
    </script>
</body>
</html>
