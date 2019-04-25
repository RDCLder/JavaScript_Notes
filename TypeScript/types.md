# Types

## Basic Types

- Boolean
  - true/false value
  - Syntax
  ```js
  const foo: boolean = value
  ```
  - e.g.
  ```js
  let isDone: boolean = false;
  ```

- Number
  - Any floating point value
    - Hexadecimal, decimal, binary, and octal literals
  - Syntax
    ```js
    const foo: number = value
    ```
  - e.g.
    ```js
    let decimal: number = 6;
    let hex: number = 0xf00d;
    let binary: number = 0b1010;
    let octal: number = 0o744;
    ```

- String
  - Any textual datatype enclosed in quotes ```'``` ```"``` or backticks `
  - Syntax
    ```
    const foo: string = value
    ```
  - e.g.
    ```js
    let color: string = "blue";
    color = 'red';
    ```
    ```js
    let sentence: string = `Hello, my name is ${ fullName }.

    I'll be ${ age + 1 } years old next month.`;
    ```

- Array
  - Array of values of the same type or multiple types
  - Syntax: 
    - Arrays with a single type
      ```js
      const foo: type[]
      ```
    - Arrays with multiple types
      ```
      const foo: (type|type)[]
      ```
  - e.g.
    - Type of element followed by []
      ```js
      let list: number[] = [1, 2, 3];
      ```
    - Generic array type ```Array<elemType>
      ```js
      let list: Array<number> = [1, 2, 3];
      ```
    - Multiple types
      ```js
      const foo: (string|number)[] = [1, "message"];
      ```

- Tuple
  - Express an array with a fixed number of elements with known types
  - Syntax
    ```js
    const foo: [type, type] = value
    ```
  - e.g.
    - A pair of a string and a number
      ```js
      // Declare a tuple type
      let x: [string, number];
      // Initialize it
      x = ["hello", 10]; // OK
      // Initialize it incorrectly
      x = [10, "hello"]; // Error
      ```
    - Accessing an element with a known index retrieves the correct type
      ```js
      console.log(x[0].substr(1)); // OK
      console.log(x[1].substr(1)); // Error, 'number' does not have 'substr'
      ```
    - Accessing an element outside the known index uses a union type
      ```js
      x[3] = "world"; // OK, 'string' can be assigned to 'string | number'

      console.log(x[5].toString()); // OK, 'string' and 'number' both have 'toString'

      x[6] = true; // Error, 'boolean' isn't 'string | number'
      ```
  

## Advanced Types

- Any
  - Represents any JavaScript value
  - Use ```any``` or leave type off
