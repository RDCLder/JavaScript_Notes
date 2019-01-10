# Node.js

## General

- Node.js is an open-source, cross-platform runtime environment used for development of server-side web applications.
  - Node exports Chrome's V8 JavaScript engine combined with some libraries for I/O and networking functionality
    - JavaScript is traditionally only client-side on the browser
    - Node allows for JavaScript to be run on the server-side (e.g local computers) as well.
  - Based on an event-driven architecture & non-blocking I/O API that is designed to optimize an application through output and scalability for real-time web applications
  - The node package ecosystem, npm, is the largest for open source libraries in the world.

- Why use Node
  - Node allows for JavaScript to be run outside of a browser on the server-side (e.g local computers).
  - Handling of Concurrent Requests
    - Asynchronous event-driven I/O helps concurrent request handling
      - If a request is received by Node for some I/O operation, it will execute the operation in the backround and continue with processing other requests.
      - For other languages, an I/O block causes the entire program to wait for the I/O operation to finish first.
    - Capable of handling concurrent connections with minimal overhead on a single process
  - Node is an open-source framework with a large, active community.
  
- When to use Node
  - Node is effective for handling high levels of concurrency and requests that do not require high computation.
    - "Light" I/O requests
  - Examples
    - Chat applications
    - Game servers
    - Collaborative environment
    - Advertisement servers
    - Streaming servers
    
- When to not use Node
  - Node is structured to be single-threaded. If a request requires computation, it slows down the whole thread process.
  - Examples
    - Mathematical calculations
    - Image resizing
    - JSON parsing
    - Regular expressions

- Node Callbacks
  - The first argument of the callback is reserved for an error object.
    - If an error occurs, it is returned by the first argument.
  - The second argument of the callback is reserved for response data.
  - Syntax
    ```js
    fs.readFile('/foo.txt', function(err, data) {
      // Error Handling
      console.log(data);
    });
    ```
  - e.g.
    ```js
    fs.readFile('/foo.txt', function(err, data) {
      if (error) {
        console.error(error.message);
        return; // Exit out of function if error occurs
      }
      console.log(data);
    });
    ```
    
## Modules

- A module in Node.js is a specific functionality organized in one or more JavaScript files which can be reused throughout the Node.js application.
  - Each module in Node.js has its own context, so it cannot interfere with other modules or pollute global scope.
  - Each module can be placed in a separate .js file under a separate folder.
  - Consider modules to be the same as JavaScript libraries.

- Node Module Pattern
  - Node modules must be imported to a file with a **require** statement.
    - Syntax
      ```js
      var module = require("moduleName");
      ```
      - The module can have any name, but the convention is to use the same name as the module being imported.
    - e.g.
      ```js
      var request = require("request");
      ```
  - Functions, objects, variables, and literals can be exported as a separate module.
    - Syntax
      ```js
      module.exports = variable/function/object;
      
      // OR
      
      exports = variable/function/object;
      ```
    - e.g.
      ```js
      // Exporting an Object
      
      module.exports = {
        firstName: "James",
        lastName: "Bond"
      };
      
      // Exporting a Function
      
      module.exports = function (msg) { 
        console.log(msg);
      };
      
      // Exporting Function as a Class
      
      module.exports = function (firstName, lastName) {
        this.firstName = firstName;
        this.lastName = lastName;
        this.fullName = function () { 
          return this.firstName + ' ' + this.lastName;
        } 
      };
      ```

- Module Types
  - Core Modules:  Built-in modules that include the bare minimum functionalities of Node.
    - e.g. DNS, File System, Path, Readline
  - Local Modules: Modules created locally in your Node.js application.
    - Local moduels can be imported using **require** with the module's local path.
    - These modules include different functionalities of your application in separate files and folders.
    - You can also package it and distribute it via NPM, so that Node.js community can use it.
  - Third Party Modules: Modules that must be installed from non-local sources.
    - Can be installed with ```npm install moduleName```

## Project Setup

- Every Node project must be setup in a specific way
  - Perform ```npm init``` for the project directory
  - Install exterior modules as needed
  - Use ```require``` to import all necessary modules
  - Establish a server if the project has web-based dependencies
  
- Setting up a server
  - Steps
    - Import node.js core module
    - Create server
    - Listen for incoming requests
  - Syntax
    ```js
    var http = require("http"); // Step 1

    var server = http.createServer((request, response) => { // Step 2
      // Handle incoming requests here
    });

    server.listen(number); // Step 3
    // Listen for incoming requests
    ```
  - e.g.
    ```js
    var http = require('http');
    
    var myServer = http.createServer(function (req, res) {
      res.writeHead(200, {'Content-Type': 'text/html'});
      res.write("The date and time are currently: " + dt.toDateString());
      res.end();
    }).listen(8080);
    ```
    
## Common Modules

### File System (fs) Module

- [Documentation](https://nodejs.org/dist/latest-v10.x/docs/api/fs.html#fs_file_system)

- The File System module provides a way of working with the computer's file system. 
  - ```var fs = require("fs");```

- **fs.unlink()**
  - Deletes a file
  - e.g.
    ```js
    var fs = require('fs');
    
    fs.unlink('/tmp/hello', (err) => {
      if (err) throw err;
      console.log('successfully deleted /tmp/hello');
    });
    ```

- **fs.readFile()**
  - Reads the content of a file
  - e.g.
    ```js
    var fs = require('fs');
    
    fs.readFile(filename, function (error, buffer) {
      if (error) {
        console.error(error.message);
      return;
      }
      console.log('File Data: ', buffer.toString());
    });
    ```
    
- **fs.writeFile()**
  - Writes data to a file
  - e.g.
    ```js
    fs.writeFile(filename, 'I love Node', function (error) {
      if (error) {
        console.error(error.message);
        return;
      }
      console.log('File Save: ', filename);
    });
    ```

### Readline Module

- [Documentation](https://nodejs.org/dist/latest-v10.x/docs/api/readline.html)

- The Readline module provides a way of reading a datastream, one line at a time.
  - ```var readline = require("readline");

- **readline.createInterface()**
  - Creates a user interface in which the user can input data
  - e.g.
    ```js
    var rl = readline.createInterface({
      input: process.stdin,
      output: process.stdout
    });
    ```

- **readline.question()**
  - Displays a query and waits for a user input.  The input is invoked in a callback function.
  - e.g.
    ```js
    rl.question("How's it going? ", function(answer) {
      console.log("Awesomesauce:", answer);
      rl.close();
    });
    ```
