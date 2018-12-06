# Higher Order Functions

## Function Fundamentals

- Definition
  - Syntax
  ```javascript
  function funcName (parameters) {
    code block
    return value
  ```
    - ```function``` and ```return``` and reserved words that specifically pertain to functions.
    - ```parameters``` and ```return``` statement are optional and ```undefined``` by default.
    - ```code block``` defines what the function does

- How functions are called
  - Functions are called using ```functionName(argument)```
  - The input arguments (if needed) are enclosed in the parentheses.
    - Inputs can be variables or values.
  - Function will be evaluated and "replaced" with the return value.
  
- Functional Declaration vs Expression
  - Functions are declared with they are first defined.
  - Functions are expressed when they are called after being declared.

- Self-invoking Function
  - Functions can be made "self-invoking"
  - Syntax:
  ```javascript
  (function () {
    code block
  })();
  ```
    - The function definition is enclosed in parentheses
    - The function definition is followed by parentheses
  - Function expressions execute automatically if the expression is followed by ().
  
- Variable Mutability in Functions
  - JS has both pass-by-value (immutable) and pass-by-reference (mutable) variables.
  - Pass-by-value
    - Strings
    - Numbers
  - Pass-by-reference (verify these)
    - Arrays
    - Objects
    - Functions
    
- ```var``` vs. ```let```
  - ```var``` is globally scoped.
  - ```let``` is block-scoped.
  
---

## Anonymous & Callback Functions

