# Miscellaneous

## Error Catching

- Try, Catch, Finally
  - Try
    - Specify the code that might throw an exception within the ```try``` block.
    - If an exception occurs in this section of code, control is passed to the corresponding ```catch``` block.
  - Catch
    - The ```catch``` block contains an alternate set of code to execute with an exception is thrown.
    - The block takes the error object as an optional parameter.
  - Finally
    - The ```finally``` block will run no matter what.
      - Even if the ```try``` or ```catch``` blocks have used the ```return``` keyword.
      
- Syntax:
  ```javascript
  try {
    // This block contains the code that can return an exception and call the catch block
  }
  catch {
    // If there is an exception, this block runs
  }
  finally {
    // This block is always executed
  }
  ```
  
- Example
  ```javascript
  <p id="demo"></p>

  <script>
  try {
      adddlert("Welcome guest!");
  }
  catch(err) {
      document.getElementById("demo").innerHTML = err.message;
  }
  </script>
  ```

- Error Object
  - A built-in object that provides error information when an error occurs.
    - Provides an error name and a message.
  - Built-in Objects
    - EvalError: An error has occured in the eval() function.
    - RangeError: An index is out of range.
    - RefereneError: A reference to be an undeclared variable has been made.
    - SyntaxError: Syntax is missing or incorrect.
    - TypeError: An illegal data type is used.
    - URIError: An error in encodeURI() has occurred.
    
## Local Storage

