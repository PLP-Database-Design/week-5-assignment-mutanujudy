# Database Interacation in Web Applications

This demonstrates the cconnection of MySQL database and Node.js to create a simple API

## Requirements
- [Node.js](https://nodejs.org/) installed
-  MySQL installed and running
-  A code editor, like [Visual Studio Code](https://code.visualstudio.com/download)

## Setup
1. Clone the repository
2. Initialize the node.js environment
   ```
   npm init -y
   ```
3. Install the necessary dependancies
   ```
   npm install express mysql2 dotenv nodemon
   ```
4. Create a ``` server.js ``` and ```.env``` files
5. Basic ```server.js``` setup
   <br>
   
   ```js
   const express = require('express')
   const app = express()

   
   // Question 1 goes here
   // Route to retrieve all patients
   app.get('/patients', (req, res) => {
      db.query('SELECT patient_id, first_name, last_name, date_of_birth FROM patients', (err, results) => {
         if (err) {
               console.error(err);
               res.status(500).send('Error retrieving patients');
         } else {
               res.json(results); // Respond with JSON data
         }
      });
   }); //and adding date_of_birth in the data.ejs file
   


   // Question 2 goes here
   // Endpoint to retrieve all providers
   app.get('/providers', (req, res) => {
      // Retrieve data from the providers table
      db.query('SELECT first_name, last_name, provider_specialty FROM providers', (err, results) => {
         if (err) {
               console.error(err);
               res.status(500).send('Error retrieving providers');
         } else {
               // Render the providers data using EJS
               res.render('providers', { results: results });
         }
      });
   });  // then created providers.ejs file inside views folder and updated it to display providers details


   // Question 3 goes here
   // Endpoint to filter patients by first name
   app.get('/data', (req, res) => {
      const firstName = req.query.first_name; // Get the first name from query parameters

      // Validate that a first name was provided
      if (!firstName) {
         return res.status(400).send('First name query parameter is required.');
      }

      // Retrieve patients with the specified first name from the database
      db.query('SELECT * FROM patients WHERE first_name = ?', [firstName], (err, results) => {
         if (err) {
               console.error(err);
               return res.status(500).send('Error retrieving patients');
         }

         // Render the filtered patient data using EJS
         res.render('data', { results: results });
      });
   });

   


   // Question 4 goes here
   // Endpoint to filter providers by specialty
   app.get('/providers', (req, res) => {
      const specialty = req.query.specialty; // Get the specialty from query parameters

      // Validate that a specialty was provided
      if (!specialty) {
         return res.status(400).send('Specialty query parameter is required.');
      }

      // Retrieve providers with the specified specialty from the database
      db.query('SELECT first_name, last_name, provider_specialty FROM providers WHERE provider_specialty = ?', [specialty], (err, results) => {
         if (err) {
               console.error(err);
               return res.status(500).send('Error retrieving providers');
         }

         // Render the filtered provider data using EJS
         res.render('providers', { results: results });
      }); 
   }); // then access the template using this 'http://localhost:3300/providers?specialty=Cardiology'

   

   // listen to the server
   const PORT = 3000
   app.listen(PORT, () => {
     console.log(`server is runnig on http://localhost:${PORT}`)
   })
   ```
<br><br>

## Run the server
   ```
   nodemon server.js
   ```
<br><br>

## Setup the ```.env``` file
```.env
DB_USERNAME=root
DB_HOST=localhost
DB_PASSWORD=your_password
DB_NAME=hospital_db
```

<br><br>

## Configure the database connection and test the connection
Configure the ```server.js``` file to access the credentials in the ```.env``` to use them in the database connection

<br>

## 1. Retrieve all patients
Create a ```GET``` endpoint that retrieves all patients and displays their:
- ```patient_id```
- ```first_name```
- ```last_name```
- ```date_of_birth```

<br>

## 2. Retrieve all providers
Create a ```GET``` endpoint that displays all providers with their:
- ```first_name```
- ```last_name```
- ```provider_specialty```

<br>

## 3. Filter patients by First Name
Create a ```GET``` endpoint that retrieves all patients by their first name

<br>

## 4. Retrieve all providers by their specialty
Create a ```GET``` endpoint that retrieves all providers by their specialty

<br>


## NOTE: Do not fork this repository
