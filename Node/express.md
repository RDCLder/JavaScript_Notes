# Express.js

## General

- [Documentation](http://expressjs.com/en/4x/api.html)

- Framework vs library
  - Frameworks and libraries are code/files of code that can be imported for specific applications.
    - They package specific functionalities together to allow for simplified and more efficient coding.
  - Frameworks have **inversion of control**
    - The control flow is specified by the framework (i.e. the framework calls you)
    - The user only inputs predefined areas (e.g. a madlib)
    - Frameworks can be heavy-weight or light-weight
      - Heavy-weight: does most of the work for the user
      - Light-weight: only does some of the required work and allows for greater customizability
  - Libraries have user control
    - Users can choose exactly how to use the library

- Express is an unopinionated, minimalist web framework for Node.js.
  - Compatible with most templating systems
  - Most popular web framework for Node
  - Light-weight

---

## How to Use

- Steps
  - Install and initialize
  - Set up server
  - Set up routes

- Initialization
  - In the project directory, initialize npm and install express
  ```bash
  npm init
  ```
  ```bash
  npm install express
  ```
  
  ```js
  var express = require("express");
  var app = express();
  ```
  
- Setting up server
  ```js
  app.get("/", () => {
    // Send response here
  });
  
  app.listen(serverNumber);
  ```
  
- Setting up routes
  - Routes are the URL address extensions that will render specific pages
  - All routes extend from the base URL's ```/```
    ```js
    app.get("/", (req, res) => {
      response.send(
        // Send response here
      );
    });

    app.get("/about", (req, res) => {
      response.send(
        // Send response here
      );
    });

    // Repeat this process with all additional URLs
    ```
  - Routes can have multiple handlers
    ```js
    app.get("/",
      (req, res, next) => {}, // callback function goes here
      (req, res, next) => {}, // callback function goes here
      (req, res, next) => {} // callback function goes here
    );
    ```
    - ```next``` keyword indicates that the next handler will be called
