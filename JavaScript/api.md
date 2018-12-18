# Application Programming Interface

## General

- APIs are interfaces for code/computers to interact with one another.
  - While humans use a visual interface (HTML), computers process APIs to obtain information.
  - APIs respond with data in formats like XML and JSON.
  
- **XML**:  Extended markup language.
  - XML is syntactically similar to HTML, but it does not describe presentation or structure.
  - XML encodes information as key-value pairs structured as a key tag with values nested inside.
  
- **JSON**:  JavaScript object notation.
  - JSON is syntactically the same as pure JavaScript object syntax except "keys" require quotes.
  - JSON encodes information as traditional key-value pairs nested in layers of objects.

- **.JSON.stringify()**
  - Utility:  Converts a JavaScript object into a string formatted using JSON.
    - Allows for sending JavaScript objects from browser to application.

- **.JSON.parse()**
  - Utility:  Processes a string containing JSON data and converts it into a JavaScript object.
    - Allows for sending strings from application to browser.

- AJAX
  - AJAX stands for asynchronous JavaScript and XML.
  - Utility:  AJAX allows for making changes to pages without reloading.
    - Pre-built HTML fragments (including whole pages)
    - Data retrieved from elsewhere on the server
    - Data from anywhere
    
- XHR
  - XHR stands for XMLHttpRequest.  XHR is an API in the form of an object that transfers data between a web browser and a web server.
    - The object is provided by the browser's JavaScript environment.
    - Retrieval of data from XHR for continuous modifying a loaded web page is the underlying concept of AJAX.
    
## JSON With jQuery

- Syntax
  ```js
  $.get(url)
  .done(function(result) {
    // Code for using data
  })
  .addFuncName(function(result2) {
    // Code for additional function
    // result2 is the result of the previous function
  })
  ... // Can chain on additional functions as needed
  ```
  - Additional functions can be chained on that execute under specific conditions

- Additional Functions
  - **.done()**:  Function block that runs when the previous block is completed successfully
  - **.fail()**:  Function block that runs when the previous block throws an error
  - **.always()**:  Function that always runs when the previous block is complete
