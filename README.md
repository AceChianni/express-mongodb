# MongoDB + Express Project

This project demonstrates how to set up a basic Express application with MongoDB Atlas, connect to the database using Mongoose, and deploy the application on Render.

---

## Table of Contents

- [Introduction](#introduction)
- [Prerequisites](#prerequisites)
- [Setup Instructions](#setup-instructions)
  - [MongoDB Atlas Setup](#mongodb-atlas-setup)
  - [Express Application Setup](#express-application-setup)
  - [Environment Variables](#environment-variables)
  - [Testing Locally](#testing-locally)
- [Deployment](#deployment)
- [License](#license)

---

## Introduction

This project uses:
- **MongoDB Atlas**: A cloud-hosted NoSQL database.
- **Express.js**: A minimal and flexible Node.js web application framework.
- **Mongoose**: An ODM (Object Data Modeling) library for MongoDB and Node.js.
- **dotenv**: To manage environment variables securely.

---

## Prerequisites

Ensure you have the following installed on your system:
- [Node.js](https://nodejs.org/) (v14 or later)
- npm (comes with Node.js)
- A free [MongoDB Atlas](https://www.mongodb.com/cloud/atlas) account
- A [Render](https://render.com/) account for deployment

---

## Setup Instructions

### MongoDB Atlas Setup

1. **Create a Cluster**:
   - Log in to [MongoDB Atlas](https://www.mongodb.com/cloud/atlas).
   - Create a cluster using the free tier and select a preferred cloud provider and region.

2. **Create a Database User**:
   - Navigate to **Database Access** in the dashboard.
   - Add a new user with a username and password.

3. **Whitelist Your IP Address**:
   - Go to **Network Access**.
   - Add your current IP address (or allow access from anywhere).

4. **Copy the Connection String**:
   - Go to **Clusters**, click **Connect**, and choose **Connect Your Application**.
   - Select **Node.js** and version **3.6 or later**.
   - Copy the provided connection string.

---

### Express Application Setup

1. **Initialize the Project**:
   ```bash
   mkdir express-mongodb
   cd express-mongodb
   npm init -y
   npm install express mongoose dotenv
   ```

2. **Create the Server**:
   - Create a file named `index.js` with the following content:

     ```javascript
     const express = require('express');
     const mongoose = require('mongoose');
     const dotenv = require('dotenv');

     dotenv.config(); // Load environment variables

     const app = express();
     const port = 3000;

     // Middleware to parse JSON bodies
     app.use(express.json());

     // Connect to MongoDB
     mongoose
       .connect(process.env.MONGO_URI, {
         useNewUrlParser: true,
         useUnifiedTopology: true,
       })
       .then(() => {
         console.log('Connected to MongoDB');
       })
       .catch((error) => {
         console.error('Error connecting to MongoDB:', error);
       });

     app.get('/', (req, res) => {
       res.send('Hello, World!');
     });

     app.listen(port, () => {
       console.log(`Server is running at http://localhost:${port}`);
     });
     ```

3. **Install Nodemon (Optional)**:
   ```bash
   npm install --save-dev nodemon
   ```

4. **Add a .gitignore File**:
   Create a `.gitignore` file with the following content:
   ```plaintext
   node_modules/
   .env
   ```

---

### Environment Variables

1. **Create a .env File**:
   - In the project root, create a `.env` file and add your MongoDB connection string:
 

2. **Load Environment Variables**:
   - Ensure `dotenv` is properly set up in `index.js` as shown above.

---

### Testing Locally

1. **Run the Server**:
   ```bash
   npx nodemon index.js
   ```

2. **Verify the Connection**:
   - Check the console for `Connected to MongoDB`.
   - Visit [http://localhost:3000/](http://localhost:3000/) in your browser to see `Hello, World!`.

---

## Deployment

1. **Create a Render Account**:
   - Sign up at [Render](https://render.com/).

2. **Deploy the Application**:
   - Link your GitHub repository containing this project.
   - Set the environment variables on Render:
     - Key: `MONGO_URI`
     - Value: `<MongoDB connection string>`

3. **Test the Deployment**:
   - Navigate to the provided URL to confirm the app is running.

---

## License

This project is licensed under the MIT License. See `LICENSE` for details.
