# ECMA Script 6

## Variable Identifiers

- ```let``` and ```const```
  - Both are block-scoped, variable identifiers
  - ```let``` is for variables with values that will change over time.
    - Best practice:  Use it inside of blocks denoted by ```{}```.
    - ```let``` vs ```var```: Leave var in legacy code to denote that the variable needs to be carefully refactored.
  - ```const``` is for variables that cannot be reassigned.
    - e.g. ```const = 3.14 // Value of Pi cannot change.```

---

## Template Literals

- Template Literals
  - Backtick character ``` ` ``` can be used to denote that a string lasts multiple lines.
  
- Interpolation
  - Enclosing a string with backticks ``` ` ``` will allow us to log variables directly into a string.
  - Syntax: console.log(`string ${varName1} string`)
  - e.g.
    ```javascript
    var name = "Pumpkin";
    console.log("My cat is named " + name + ".");
    
    // This is equivalent to:
    
    console.log(`My cat is named ${name}.`);
    ```
- New lines do not need to be explicitly declared.
  - e.g.
    ```javascript
    var text = (
      "cat\n" +
      "dog\n" +
      "nickelodeon"
    );

    // This is equivalent to:

    var text = (
      `cat
      dog
      nickelodeon`
    );
    ```
    
- Template literals can accept expressions
  - e.g.
    ```javascript
    let today = new Date();
    let text = `The time and date is ${today.toLocaleString()}`;
    ```
---

## Destructuring

- Destructuring allows us to extract values from arrays and objects (even nested) and store them in variables with a more convenient syntax.
  - Arrays
    - ES5
      ```javascript
      var arr = [1, 2, 3, 4];
      var a = arr[0];
      var b = arr[1];
      var c = arr[2];
      var d = arr[3];
      ```
      
    - ES6
      ```javascript
      let [a, b, c, d] = [1, 2, 3, 4];
      console.log(a); // 1
      console.log(b); // 2
      
      // This is equivalent to a, b, c, d = 1, 2, 3, 4 in Python
      ```
      
  - Objects
    - ES5
      ```javascript
      var luke = {occupation: "jedi", father: "anakin"};
      var occupation = luke.occupation; // "jedi"
      var father = luke.father; // "anakin"
      ```
      
    - ES6
      ```javascript
      let luke = {occupation: "jedi", father: "anakin"};
      let {father, occupation} = luke;
      
      console.log(occ); // "jedi"
      console.log(dad); // "anakin"
      ```
      - Notice that even though the positions of ```father``` and ```occupation``` were switched for the assignment, they still retain their corresponding values.
      - This is because objects (or dictionaries in Python) are indexed only by key names and not by position or numbers.

---
      
## Functions

- Arrow Function
  - An arrow function expression has shorter syntax than a traditional function expression and does not have
    - ```this```
    - ```arguments```
    - ```super```
    - ```new.target```
  - Utility
    - Arrow functions are used for non-method functions and cannot be used as constructors.
    - There is no binding of arguments
  - Syntax
    - General
      ```javascript
      (param1, param2, ..., paramN) => {statements}
      ```
    - Conditional (Ternary) Operator
      ```javascript
      (arguments) => {return (condition) ? output1 : output2}
      
      // This is equivalent to 
      
      (arguments) => {
        if (condition == true) {
          return output1
        }
        else {
          return output2
        }
      }
      ```
      
  - Examples
    - General
      ```javascript
      var materials = [
        'Hydrogen',
        'Helium',
        'Lithium',
        'Beryllium'
      ];

      console.log(materials.map(material => material.length)); // outputs [8, 6, 7, 9]
      ```
    - Ternary Operator Example
      ```javascript
      // General

      function(a){
          if(a < 10){
              return 'valid';
          }else{
              return 'invalid';
          }
      }

      // Using Ternary Operator

      (a) => {(a < 10) ? 'valid' : 'invalid'}
      ```

    - Multiple Ternary Operators Example
      ```javascript
      // General

      function getIcon(area) {
        if (area == 1) { 
          return icon1; 
        } else if (area == 2) { 
          return icon2; 
        }

        return icon0;
      }

      // Using Ternary Operator

      icon: (area == 1) ? icon1 : (area == 2) ? icon2 : icon0
      ```

- JavaScript ```this``` vs Python ```self```
  - Python ```self```: An instance of the current object in the class method.
  - JavaScript ```this```: Current execution context of a function.
  
- JavaScript inherently supports prototype-based object-oriented programming
  - ES6 has updated the OOP syntax to more closely follow other class-based OOP
  - ES5
    ```javascript
    function getType() { // doesn't work in ES6
      setTimeout(function () {
        console.log('Type is: ' + this.type);
      }, 500);
    }
    ```
    
  - ES6
    ```javascript
    function selfGetType() {
      var self = this;
      setTimeout(() => {
        console.log('Type is: ' + self.type);
      }, 500);
    }
    ```
    - ```this``` becomes replaced with ```self```
    
- Default Parameters
  - ES5
    ```javascript
    function addTwoNumbers(x, y) {
      x = x || 0;
      y = y || 0;
      return x + y;
    }
    ```
  
  - ES6
    ```javascript
    function addTwoNumbers(x=0, y=0) {
      return x + y;
    }
    addTwoNumbers(2, 4); // 6
    addTwoNumbers(2); // 2
    addTwoNumbers(); // 0
    ```
    
- Rest Parameters
  - If a function has an indefinite amount of arguments, we can use the ```...args```
  - ES5
    ```javascript
    function logArguments() {
      for (var i=0; i < arguments.length; i++) {
          console.log(arguments[i]);
      }
    }
    ```
  - ES6
    
    ```javascript
    function logArguments(...args) {
      for (let arg of args) {
          console.log(arg);
      }
    }
    ```
---
    
## Classes

- Prior to ES6, "classes" were implemented by creating a constructor function and adding properties by extending the prototype:
  - ES5
    ```javascript
    function Person(name, age, gender) {
      this.name   = name;
      this.age    = age;
      this.gender = gender;
    }
    Person.prototype.incrementAge = function () {
      return this.age += 1;
    };
    ```
  - ES5 Extended Classes
    ```javascript
    function Personal(name, age, gender, occupation, hobby) {
      Person.call(this, name, age, gender);
      this.occupation = occupation;
      this.hobby = hobby;
    }
    Personal.prototype = Object.create(Person.prototype);
    Personal.prototype.constructor = Personal;
    Personal.prototype.incrementAge = function () {
      Person.prototype.incrementAge.call(this);
      this.age += 20;
      console.log(this.age);
    };
    ```
- ES6 has updated OOP syntax to more closely resemble the syntax of other class-based OOP languages (e.g. Python)
  - ES6
    ```javascript
    class Person {
      constructor(name, age, gender) {
          this.name   = name;
          this.age    = age;
          this.gender = gender;
      }
      incrementAge() {
        this.age += 1;
      }
    }
    ```
  - ES6 Extended Classes
    ```javascript
    class Personal extends Person {
      constructor(name, age, gender, occupation, hobby) {
          super(name, age, gender);
          this.occupation = occupation;
          this.hobby = hobby;
      }
      incrementAge() {
          super.incrementAge();
          this.age += 20;
          console.log(this.age);
      }
    }
    ```
