# User Sessions

## General

- Webpages have no memories
  - A user going from page to page will be treated as a new visitor each time.
  - Session cookies enables a website to keep track of the user's movement histry across the website.
  - Cookies allow users to proceed through a website quickly and easily without the need to re-authenticate on every page.
  
- Session
  - A session is a place to store data that you want access to across requests.
    - Each user has a unique session each time they visit a website.
    - Sessions can be used to temporarily store and access user data.
  - Sessions allow applications to store state information.
    - Based on what action a user took on a page, something different can happen on another page.
    - Without states, applications would not be very useful.
    
- Dependencies
  - [express-session](https://github.com/expressjs/session)
    ```js
    npm install express-session
    var session = require("express-session");
    ```
  - [cookie-parser](https://www.npmjs.com/package/cookie-parser)
    ```js
    npm install cookie-parser
    var express = require("express");
    var cookieParser = require("cookie-parser");
    var app = express();
    app.use(cookieParser());
    ```
    
- Sessions can store their information in different ways.
  - In application memory
  - In a cookie
  - In a memory cache
  - In a database
  
- Session using a cookie
  ```js
  var app = express();
  
  app.use(session({
    secret: "keyboard cat",
    resave: false,
    saveUninitialized: true,
    cookie: {secure: true, maxAge: 60000}
  }));
  ```
    - ```cookie.maxAge``` specifies the time (ms) to use when calculating the expires set-cookie attribute
    
- ```req.session```
  ```js
  var sessData = req.session;
  sessData.someAttribute = "foo";
  
  var someAttribute = req.session.someAttribute;
  ```
  
- Data Routing
  - Set session data in one route handler
    ```js
    app.use(session({ secret: 'this-is-a-secret-token', cookie: { maxAge: 60000 }}));
    
    // Access the session as req.session
    app.get('/', function(req, res, next) {
      var sessData = req.session;
      sessData.someAttribute = "foo";
      res.send('Returning with some text');
    });
    ```
  - Access it in another route handler
    ```js
    app.get('/bar', function(req, res, next) {
      var someAttribute = req.session.someAttribute;
      res.send(`This will print the attribute I set earlier: ${someAttribute}`);
    });
    ```
    
## Using a Database

- Example
  ```js
  var myStore = new SequelizeStore({
      db: connection
  })
  var app = express();
  app.use(cookieParser());
  app.use(session({
    secret: 'keyboard cat',
    store: myStore,
    resave: false, 
    proxy: true 
  }));
  ```

- Dependencies
  - pg-promise
  - sequelize
  - [connect-pg-simple](https://www.npmjs.com/package/connect-pg-simple)
    - Create a session table in database.
      ```
      psql mydatabase < node_modules/connect-pg-simple/table.sql
      ```
  - sequelize-session-store
    - Requires express application using the express-session middleware
    - Requires an instance of sequelize
    - If no model is apssed, one will be created
      ```sql
      CREATE TABLE express_session (
        sid VARCHAR NOT NULL,
        sess TEXT NOT NULL,
        expire TIMESTAMP(6) NOT NULL,
        PRIMARY KEY (sid)
      )
      ```
      
- Login Example
  ```js
  app.use(function (request, response, next) {
    if (request.session.user) {
      next();
    } else if (request.path == '/login') {
      next();
    } else {
      response.redirect('/login');
    }
  });
  ```
  ```js
  app.get('/login', function (request, response) {
    response.render('login.html');
  });
  
- Post Parsing
  ```js
  var body_parser = require('body-parser');
  app.use(body_parser.urlencoded({extended: true}));
  ```
  ```js
  app.post('/login', function (request, response) {
    var username = request.body.username;
    var password = request.body.password;
    if (username == 'aaron' && password == 'narf') {
      request.session.user = username;
      response.redirect('/');
    } else {
      response.render('login.html');
    }
  });
  ```
