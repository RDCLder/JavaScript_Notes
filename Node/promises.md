# Promises

## General

- A promise is an object that may produce a single value in the future
  - Helps avoid callback nesting (aka callback hell)
  - Consolidates error handling
  
- A promise can be in one of 3 states
  - Pending:  Executing the promise
  - Fulfilled:  Finished executing the promise
  - Rejected:  Was unable to execute the promise

- Promise Syntax
  - Standard
    ```js
    Promise.then(successCallback, errorCallback);
    ```
    ```js
    promise
      .then(successCallback)
      .catch(errorCallback);
    ```
    ```js
    promise
      .then(successCallback)
      .fail(errorCallback);
    ```
  - Chaining
    ```js
    promise
      .then(successCallback1)
      .then(successCallback2)
      .catch(errorCallback)
      .finally(cleanUpCallback);
    ```
  - Multiple Promises
    ```js
    Promise.all([promise1, promise2]).then(function () {
      console.log('Everything is done');
    });
    ```



## Promises in Other Modules

- **jQuery**
  ```js
  var api_url = 'https://api.punkapi.com/v2/beers?brewed_before=11-2012&abv_gt=6';
  var jqxhr = $.ajax(api_url)
    .done(function(data) {
      console.log(data);
    })
    .fail(function(jqXHR, textStatus, errorThrown) {
      console.error(errorThrown);
    })
    .always(function() {
      console.log("complete");
    });
  ```
  
- **fetch**
  ```js
  var myHeaders = new Headers();
  var myInit = { method: 'GET',
                 headers: myHeaders,
                 mode: 'cors',
                 cache: 'default' };
  fetch(api_url, myInit)
    .then(function(response) {
      return response.json();
    })
    .then(function(data) {
      console.log(data);
    })
    .catch(function (error) {
      console.error(error);
    });
  ```
  
- **axios**
  - Standard
    ```js
    axios.get(api_url)
      .then(function (response) {
        console.log(response.data);
      })
      .catch(function (error) {
        console.error(error);
      });
    ```
  - Multiple Promises
    ```js
    var p1 = axios.get(api_url);
    var p2 = axios.get(api_url);
    Promise.all([p1, p2])
      .then(function (responses) {
        console.log(responses[0].data);
        console.log(responses[1].data);
      });
    ```

## Custom Promises

- Making Custom Promises
  ```js
  var p = new Promise(function (resolve, reject) {
      setTimeout(function () {
        resolve('Hello');
      }, 3000);
    });
    p.then(function (value) {
      console.log('DONE: ', value);
    });
  ```
  ```js
  function fix_name (name) {
      var promise = new Promise(function (resolve, reject) {
        try {
          var new_name = name.replace('-', ' ');
          resolve(new_name);
        } catch (error) {
          reject(error);
        }
      });
      return promise;
    }
  ```
  
### Promise Modules

- [**pg-promise**](http://vitaly-t.github.io/pg-promise/index.html)
  - Integrates postgreSQL with promises
  
- [Bluebird](http://bluebirdjs.com/docs/getting-started.html)
  - Promise library that overrides default ES6 Promise
  
- Initialization
  - Install libraries
    ```
    npm install bluebird
    ```
    ```js
    const promise = require("bluebird");
    ```
  - Specify initialization options
    ```js
    const initOptions = {
      promiseLib: promise
    };
    ```
  - Database connection parameters
    ```js
        const config = {
        host: 'localhost',
        port: 5432,
        database: 'veronica2',
        user: 'postgres'
    };
    ```
  - Load pg-promise
    ```js
    const pgp = require('pg-promise')(initOptions);
    ```
  - Create database instance
    ```js
    const db = pgp(config);
    ```
    
- Database Query
  - Syntax:  ```db.method```
    - Methods
      - ```query```:  Generic query with no constraints.
      - ```one```:  Expects one row or errors out
      - ```any```:  No expectations
      - ```none```:  Expects no result or error
      - ```many```:  Expects one or more rows or error
      - ```result```:  Return the raw results (useful for insert update and deletes)
  - e.g.
    - ```db.query```
      ```js
      db.query('SELECT * FROM restaurant')
      .then(function (results)) {
        results.forEach(function (r) {
          console.log(r.id, r.name. r.address, r.category);
        });
      });
      ```
    - ```db.one```
      ```js
      db.one("SELECT * FROM restaurant WHERE name='R1'")
        .then(function (r)) {
          console.log(r.id, r.name. r.address, r.category);
        });
      ```
    - ```db.result```
      ```js
      db.result("INSERT INTO restaurant \
        VALUES (default, 'Narf')")
        .then(function (result) {
          console.log(result);
        });
      ```
  
- Close connection
  ```js
  pgp.end()
  ```
  
### Protect Your Database

- SQL Injection
  - A way to change SQL-based database data
  - Prevent with security measures
  - e.g.
    ```js
    var name = "Big Belly Burger";
    var query = `INSERT INTO restaurant \
      VALUES (default, '${name}')"`;
    db.result(query)
      .then(function (result) {
        console.log(result);
      });
    ```
    
- [Prepared Statements](https://www.linkedin.com/pulse/protecting-your-postgresql-database-from-sql-attack-rogers-iii/)
  - Account for SQL injections with pre-prepared statements that override outside statements
  - e.g.
    ```js
    var q = "INSERT INTO restaurant VALUES (default, $1)";
    db.result(q, name)
      .then(function (result) {
        console.log(result);
      });
    ```
    ```
    var biz = {name: "Lard Lad Donuts"};
    var q = "INSERT INTO restaurant \
      VALUES (default, ${name})";
    db.result(q, biz)
      .then(function (result) {
        console.log(result);
      });
    ```
