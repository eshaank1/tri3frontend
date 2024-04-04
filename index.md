---
layout: default
title: Student Blog
---
<html lang="en">
<style>
  /* Importing Google Fonts */
@import url('https://fonts.googleapis.com/css2?family=Black+Ops+One&family=Roboto:wght@300&display=swap');

/* Button template */
.button {
  width: auto;
  height: auto;
  border-radius: 10px;
  background-color: #21807c;
  border: 3px solid #F748A9;
  font-size: 1.5em;
  display: flex;
  justify-content: center;
  align-items: center;
  grid-column: span 1;
  grid-row: span 1;
  transition: all 0.5s;
}

/* Darkens the background color on hover to create a selecting effect */
.button:hover {
  background-color: #F748A9;
}

/* "row style" is flexible size and aligns pictures in center */
.row {
  align-items: center;
  display: flex;
}

/* "column style" is one-third of the width with padding */
.column {
  flex: 16.66%;
  padding: 3px;
}

/* Calculator container */
.calculator-container {
  width: 90vw; /* this width and height is specified for mobile devices by default */
  height: 80vh;
  margin: 0 auto;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-template-rows: 0.5fr repeat(4, 1fr);
  gap: 10px 10px;
}

@media (min-width: 600px) {
  .calculator-container {
      width: 40vw;
      height: 80vh;
  }
}

/* Calculator buttons styling */
.calculator-number, .calculator-operation, .calculator-clear, .calculator-equals {
  width: auto;
  height: auto;
  border-radius: 10px;
  border: 3px solid #F748A9;
  font-size: 1.5em;
  display: flex;
  justify-content: center;
  align-items: center;
  grid-column: span 1;
  grid-row: span 1;
  transition: all 0.5s;
}

.calculator-clear {
  background-color: #e68b1c;
}

.calculator-equals {
  background-color: #e70f0f;
}

/* JWT login page */
.title {
  font-size: 50px;
  font-weight: bold;
  font-family: Roboto;
  color: #F748A9;
}

.descriptiontext, .inputusername, .inputpassword {
  font-size: 30px;
  font-family: 'Black Ops One', system-ui;
  color: #FFC8C5;
}

.inputpassword {
  color: #F748A9;
}

.signup-button, .delete-button, .update-button {
  width: auto;
  height: auto;
  border-radius: 10px;
  border: 3px solid #F748A9;
  font-size: 1.5em;
  display: flex;
  justify-content: center;
  align-items: center;
  grid-column: span 1;
  grid-row: span 1;
  transition: all 0.5s;
  color: white;
}

.signup-button {
  background-color: #000000;
}

.delete-button {
  background-color: red;
}

.update-button {
  background-color: green;
}

body {
  background: url({{site.baseurl}}/images/logincar.gif);
  background-size: cover;
}

</style>
<head>
<script>
    //import { uri, options } from '{{site.baseurl}}/assets/js/api/config.js';

    function login_user() {
      const enteredUid = document.getElementById("uid").value;
      const enteredPassword = document.getElementById("password").value;
      console.log("Uid = " + enteredUid)
      console.log("Password = " + enteredPassword)
      const signupHeaders = new Headers();
      signupHeaders.set('111', '222');
      
      signupHeaders.set("Accept", "*/*");
      signupHeaders.set("Accept-Language", "en-US,en;q=0.9");
      signupHeaders.set("Content-Type", "application/json");

      login_api(enteredUid,enteredPassword)
        
      }
    

    function login_api(uid, pw){
      var myHeaders = new Headers();
      myHeaders.append("Accept", "*/*");
      myHeaders.append("Accept-Language", "en-US,en;q=0.9");
      myHeaders.append("Content-Type", "application/json");
      //myHeaders.append("Cookie", "jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJfdWlkIjoidG9ueSJ9.jEShka0oXI1-uCuSTfo3ed5WRw3ASLNV0Tpn1kc5GB0");
      myHeaders.append("Authorization", "Bearer eyJhbGciOiJIUzI1NiJ9.e30.BSQAHTECtxHe2dzC75Ijpz18pTmjDb1q6WWrJMOLlm0");
      myHeaders.append("Cookie", "jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJfdWlkIjoibWJhNCJ9.oBlUf7JKmb_rLaoAFJ55yUs-70O7NUAFE6ALOXOviUc");

var raw = "";

var requestOptions = {
  method: 'GET',
  headers: myHeaders,
  body: raw,
  redirect: 'follow'
};

fetch("http://127.0.0.1:8058/api/users", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));

      var raw = JSON.stringify({
          "uid": uid,
          "password": pw
        });

      var requestOptions = {
          method: 'POST',
          headers: myHeaders,
          body: raw,
          redirect: 'follow'
        };

      fetch("http://127.0.0.1:8058/api/users/authenticate", requestOptions)
          .then(response => {
            if (response.ok) {
                console.log("User logged in successfully");
                window.location.href = "{{site.baseurl}}/main"

              } else {
                console.error("User login failed");
                // You can handle failed login attempts here
                const errorMessageDiv = document.getElementById('errorMessage');
                errorMessageDiv.innerHTML = '<label style="color: red;">User Login Failed</label>';
              }
          })
          .then(result => { 
            console.log(result);
            
            })
          .catch(error => console.log('error', error));
          

      
      //return response
    }


  </script>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Login Page</title>
  <link rel="stylesheet" href="styles.css"> <!-- Include the compiled CSS file -->
</head>

<body>
  <!-- Your HTML login form -->
  <div id="errorMessage"></div>
  <form action="javascript:login_user()">
    <p><label for="uid">User ID:</label>
      <input type="text" name="uid" id="uid" required>
    </p>
    <p><label for="password">Password:</label>
      <input type="password" name="password" id="password" required>
    </p>
    <p>
     <button class="button-spacing">Log In</button>
          <button onClick = "window.location.href ='{{site.baseurl}}/signup'" class="button-spacing" >Sign Up</button>

      
    </p>
  </form>

  <!-- Your JavaScript code -->
  
</body>

</html>