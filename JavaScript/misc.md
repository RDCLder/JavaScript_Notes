# Miscellaneous

## Closures



## Regular Expressions

- General
  - A regular expression searches for characters that form a pattern.
    - It can replace those characters with new ones.
  - A regular expression is a type of object.
    - Constructed with the RegExp constructor
  - Syntax
    - Creating a RegExp
      ```javascript
      let pattern = new RegExp("pattern");
      pattern.RegExpMethod(argument);

      // OR

      /pattern/.RegExpMethod(argument);
      ```
        - RegExp methods determine what to do with the argument.
    - Pattern-matching
      - ```a``` - matches one character that is ```a```
      - ```abc``` - matches ```a```, followed by ```b```, followed by ```c```
      - ```a*``` - matches ```a``` 0 or more times (```+``` matches 1 or more times)
      - ```[^a]``` - matches one character that is not a
      - ```a{n1, n2}``` - mathes a n1 to n2 times and no less or more
      - [Others](https://www.debuggex.com/cheatsheet/regex/javascript)
      
- RegExp Methods
  - ```exec()```:  Tests for a match in a string.  Returns the first match.
  - ```test()```:  Tests for a match in a string.  Returns true or false.
  - ```toString()```:  Returns the string value of the regular expression.

- Common Pattern Shortcuts
  - ```\d```:  Any digit character
  - ```\w```:  An alphanumeric character
  - ```\s```:  Any whitespace character (e.g. space, tab, newline, etc.)
  - ```\D```:  A nondigit character
  - ```\W```:  A nonalphanumeric character
  - ```\S```:  A nonwhitespace character
  - ```.```:  Any character except for newline
  
- Common Regular Expressions
  - ```/^\d+$/```:  A number
  - ```/^[\s]+/```:  Whitespace at start of line
  - ```/[^@]+@[^@]+/```:  Email
  - ```/^#[a-fA-F0-9]{6}$/```:  Hex color value
  - ```/^(\d{2}\/\d{2}\/\d{4})|(\d{4}=\d{2}-\d{2})$/```: Date (YY-MM-DD)

- Examples
  ```javascript
  /e/.exec("The best things in life are free.") // Returns the first e
  /abc/.test("abcde") // true
  /abc/.test("abxde") // false
  ```

---

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

