---
permalink: /scholarsearch
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
            let colleges = [];

            function fetchColleges() {
                fetch("http://127.0.0.1:8058/dataList")
                    .then(response => response.json())
                    .then(result => {
                        colleges = result; // Assuming result is an array of colleges
                        console.log(colleges); // Debug: Log to console
                    })
                    .catch(error => console.error('Error fetching colleges:', error));
            }

            function performSearch(query) {
                searchResults.innerHTML = ''; // Clear previous results

                if (query.trim() === '') {
                    searchResults.innerHTML = '<p>Please enter a search term.</p>';
                    return;
                }

                const filteredResults = colleges.filter(college => college.name.toLowerCase().includes(query.toLowerCase()));

                if (filteredResults.length > 0) {
                    filteredResults.forEach(college => {
                        const resultDiv = document.createElement('div');
                        resultDiv.classList.add('searchResult');
                        resultDiv.innerHTML = `
                            <h3>${college.name}</h3>
                            <p>${college.description}</p>
                        `;
                        searchResults.appendChild(resultDiv);
                    });
                } else {
                    searchResults.innerHTML = '<p>No results found.</p>';
                }
            }

            searchForm.addEventListener('submit', function(event) {
                event.preventDefault(); // Prevent the form from submitting normally
                performSearch(searchInput.value);
            });

            fetchColleges();
        });
    </script>
</body>
</html>
