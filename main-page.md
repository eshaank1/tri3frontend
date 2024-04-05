---
permalink: /main
---
<html>
<head>
    <title>Links to projects</title>
    <style>
        /* Table styling with a purple theme */
        table {
            border-collapse: collapse;
            width: 100%;
            box-shadow: 0 2px 15px rgba(128, 0, 128, 0.2); /* Shadow with a purple hue */
            margin-top: 20px;
            background-color: #f2e6ff; /* Light purple background */
        }
        th, td {
            border: 1px solid #d3bced; /* Softer purple border */
            padding: 8px 20px;
            text-align: left;
            background-color: #e6ccff; /* Slightly darker purple for contrast */
        }
        th {
            background-color: #c29bff; /* Darker purple for headers */
            color: #006400;
        }
        tr:nth-child(even) {background-color: #f2e6ff;} /* Alternating rows a lighter purple */
        tr:hover {background-color: #d9b3ff;} /* Hover color in purple */

        /* Button styling with a blue theme */
        button {
            padding: 10px 15px;
            background-color: #007bff; /* Blue background */
            color: #006400;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        button:hover {
            background-color: #0056b3; /* Darker blue on hover */
        }

        /* First column text styling */
        td:first-child, th:first-child {
            color: #006400; /* Dark green text */
        }

        /* Body background GIF */
        body {
            background-image: url('{{site.baseurl}}/images/logincar.gif'); /* Add your GIF link here */
            background-size: cover; /* Cover the entire page */
            background-position: center; /* Center the background image */
            background-repeat: no-repeat; /* Do not repeat the image */
        }
    </style>
</head>
<body>

<table>
    <tr>
        <th><b>Name/Project:</b></th>
        <th>Anagha</th>
        <th>Eshaan</th>
        <th>Ninaad</th>
        <th>Patrick</th>
        <th>Group</th>
    </tr>
    <tr>
        <td>ML titanic</td>
        <td><button onClick="window.location.href = '';">Link</button></td>
        <td><button onClick="window.location.href = '';">Link</button></td>
        <td><button onClick="window.location.href = '{{site.baseurl}}/ninaad-titanic';">Link</button></td>
        <td><button onClick="window.location.href = '/patricktitanic';">Link</button></td>
        <td><button onClick="window.location.href = '{{site.baseurl}}/anagha-titanic';">Link</button></td>
    </tr>
    <tr>
        <td>Personal ML</td>
        <td><button onClick="window.location.href = '{{site.baseurl}}/diamond';">Link</button></td>
        <td><button onClick="window.location.href = '{{site.baseurl}}/house';">Link</button></td>
        <td><button onClick="window.location.href = '{{site.baseurl}}/mpg';">Link</button></td>
        <td><button onClick="window.location.href = '{{site.baseurl}}/carcrash';">Link</button></td>
        <td><button onClick="window.location.href = '';">Link</button></td>
    </tr>
    <tr>
        <td>CPT</td>
        <td><button onClick="window.location.href = '{{site.baseurl}}/stockfetch';">Link</button></td>
        <td><button onClick="window.location.href = '{{site.baseurl}}/cryptofetch';">Link</button></td>
        <td><button onClick="window.location.href = '{{site.baseurl}}/games';">Link</button></td>
        <td><button onClick="window.location.href = '{{site.baseurl}}/match';">Link</button></td>
    </tr>
</table>

</body>

<div style="background-color:#e93e91; padding: 10px; border-radius: 20px; border: 2px solid black;">

<header><b>Plans for the Integration</b></header>
<br>
<text>
- We integrated the video sharing platform and the login system into the shared repo
<br>
<br>
- Finally, we integrated the other CPT projects
<br>
<br>
- Then, the different machine learning systems were integrated into the repo. (Titanic, Diamond cost predictor, MPG predictor, likelihood of car crash predictor, and house price predictor)
<br>
</text>
</div>
</html>
