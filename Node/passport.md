# Passport

## General

- An authentication middleware for Node.js.
  - Can be integrated with any Express-based web app
  - Supports a comprehensive set of strategies for authentication using either
    - Username and password
    - Facebook
    - Twitter
    - Much more

- Dependencies
  - passport
  - passport-local
  - cookie-Parser
  - body-parser
  - express-session
  - bcryptjs
  - sequelize
  - pg
  - pg-hstore
  - express
  
- Requires instance of sequelize
  - If a sequelize instance is not passed in, an error will be thrown.
  - If you do not pass it a model, one will be created and available for you to access using the SequelizeSessionStore instance.
  - You need an Express application using the express-session middleware
  
- connect-session-sequelize
  ```js
  var session = require('express-session'); 
  var SequelizeStore = require('connect-session-sequelize')(session.Store);
  ```
  ```js
  var myStore = new SequelizeStore({
    db: db.sequelize
  })
  app.use(session({
      secret: 'keyboard cat',
      store: myStore,
      resave: false,
      proxy: true
  }))
  myStore.sync();
  ```

## Using Passport

- Requirements for passport
  - Initialize passport
  - Local strategy
  - Express sessions
  - Deserialization/serialization
  
- Initialize passport
  ```js
  app.use(passport.initialize());
  app.use(passport.session());
  ```
  
- A form is used for the user to enter their information
  - Form action directs to the login page
  - Post method sends a post request with all relevant information
    ```html
    <form action="/login" method="post">
      <div>
        <label>Username:</label>
        <input type="text" name="username"/>
      </div>
      <div>
        <label>Password:</label>
        <input type="password" name="password"/>
      </div>
    ```
    
- Route
  - Using authenticate() with the local strategy will handle the login request.
    ```js
    app.post("/login",
      passport.authenticate("local", 
        { successRedirect: "/",
          failureRedirect: "/login",
          failureFlash: true
        }));
    ```
      - Setting failureFlash to true instructs Passport to flash an error message using the message option set by the verify callback
      - Useful when prompting the user to try again
      
- Local Strategy
  
