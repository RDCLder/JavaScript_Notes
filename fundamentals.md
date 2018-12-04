# Fundamentals

## Strings and Variables

- Commenting
  - Syntax:
    - ```/* [comment] */```
      - Useful when a comment contains line breaks.
    - ```// [comment]```
    
- Printing
  - Syntax: ```console.log("text")```
    
- General Syntax
  - Variables must be designated with the "var" command
    - Otherwise, the variable will be declared on a global scope.
  - Statements must be ended with a semicolon ```;```
  - Both numbers and strings can be concatenated.  JS considers all characters to be of the same type.
  - Blocks are denoted by ```{}```
    - e.g.
    ```javascript
    if age >= 21 {
      console.log("You get free beer!")
    }
    ```

---

## Conditional Logic

- If/else if/else
  - Syntax: ```if``` ```else if``` ```else```

- Switch Statements
  - Switch statements are for expressions that have many potential matches instead of a single match in the case of if/else if/else statements.
    - Python has if-if-if statements to perform the same logic.
  - Syntax: 
  ```
  switch (expr) {
    case value1:
      action1;
      break;
    case value2:
      action2;
      break;
    case valueN:
      actionN;
      break;
    default:
      actionDefault;
  }

---

## Flow Control

- Looping
  - While
    - Syntax:
    ```javasript
    while (statement) {
      code block
    }
    ```
    - e.g.
    ```javascript
    var count = 0;
    while (count < 10) {
      console.log(count);
      count ++ 1 // This is equivalent to count = count + 1;
    }
    ```
  - For
    - Syntax:
    ```javascript
    for (start; test; increment) {
      code block
    }
    ```
    - e.g.
    ```javascript
    for (var count = 0; count < 10; count ++) {
      console.log(count)
    }
    ```
---

## Collections

- A collection is a data structure that stores different data types.

### Arrays

- Array
  - A list of data types
  - Syntax: ```[item1, item2, item3]```
  - Elements in an array can be accessed by indexing
    - Syntax: ```array[index]``` where index ranges from 0 to length of array - 1

Array Methods
  - ```.push()```: Adds one or more elements to the end of an array and returns the new length
  - ```.pop()```: Removes the last element fro an array and returns that element.
  - ```.shift()```: Removes the first element from an array and returns that element.
  - ```.splice()```: Removes and returns the elements in an array as a new array starting at the specified beginning number up to a specified times.
    - Syntax: ```arr.splice(index, number)```
    - e.g.
    ```javascript
    var arr = [1, 2, 3, 4, 5];
    arr.splice(2, 2)
    // Starts at position 2 and returns 2 numbers: [3, 4]
    ```
  - ```.slice()```: Returns the elements in an array in the specified range.
    - Syntax: ```str.slice(start, end)```
      - Returns an array that ranges from the starting index and up to but not including the ending index.
  - ```.split()```: Splits a string based on the specified separator.
    - Syntax: ```str.split(separator, limit)```
      - If no separator is specified, the entire string is returned.
      - If a separator of just "" is used, even spaces will be separated.
      - A limit will specify how many times splitting occurs.  Remaining words are discarded.
    - e.g.
    ```javascript
    var words = "Oh hey, how's it going?".split(" ", 3);
    # This specifies splitting by space 3 times.
    # Returns ["Oh", "hey,", "how's"]
    ```
  - ```.join()```: Joins all elements of an array (or array-like object) into a string and returns the string.
    - Syntax: ```arr.join(joiner)```
      - The joiner specifies how exactly to join the elements of the array.
      - Typically, the joiner is a space for joining an array of words, but it can by any character(s).
    - e.g.
    ```javascript
    var wordArr = ["This", "is", "a", "sentence."];
    sentence = wordArr.join(" ");
    console.log(sentence);
    ```
      
- Looping through an array
  - Syntax
  ```javascript
  for (initialization; condition; final-expression) {
    code block
  }
  ```
  - e.g.
  ```javascript
  for (var i = 0; i < words.length; i += 1) {
    console.log(words[i])
  }
  ```
  
### Objects

- Object
  - Similar to a dictionary in python, an object stores key-value pairs in {}.
  - Syntax: ```var objectName {key:value, key:value};```
    - Keys must always be strings.
  - e.g.
  ```javascript
  var object1 {
    Item1: value1,
    Item2: value2,
    Item3: value3
  };
  ```

- Appending objects
  - Objects can be appended to just like dictionaries
  - Syntax: ```objectName[keyName] = newValue```

- Deleting properties from an object
  - Syntax: ```delete objectName[keyName]```

---

## Functions

- Syntax:
  ```javascript
  function fname (arguments) {
    code block
  }
  ```

- e.g.
  ```javascript
  function hello (name) {
    return "Hello " + name;
  }
  ```
