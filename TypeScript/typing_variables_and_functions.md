# Typing, Variables, and Functions

## Grammar

- Type Inference
  - TypeScript can infer variable types based on context but the best practice is to explicitly declare types
  - Process
    - Declare variable
    - Name it
    - Annotate
    - Set type
    - Set value
  - e.g.
    - JavaScript
    ```js
    var num = 2;
    var any1;
    ```
    - TypeScript
    ```js
    var num: number = 2;
    var any1: any;
    ```
    
- Static and Dynamic Typing
  - JavaScript
    - Dynamic typing
    - Type safety happens at run-time debugging
  - TypeScript
    - Static typing (optional)
    - Type safety is a compile-time feature
      - Any errors will be caught right away before the code is executed
      - e.g. declaring a variable as one type and reassigning it to a different type later on will cause an error
      
- Ambient Declarations
  - Tells compiler that the source code exists elsewhere
    - Used for external libraries (e.g. jQuery, angular, node.js)
    - File will not be transpiled to JavaScript but used for type safety and intellisense
  - Syntax: 
    - Filename
    ```Sample.d.ts```
    - File/variable declaration
    ```js
    declare module Module_Name {
    }
    ```
    - Reference
    ``` /// <reference path = " Sample.d.ts" /> ```
  - e.g.
  ```js
  FileName: CalcThirdPartyJsLib.js 
  var TutorialPoint;  
  (function (TutorialPoint) {  
     var Calc = (function () { 
        function Calc() { 
        } 
        Calc.prototype.doSum = function (limit) {
           var sum = 0; 

           for (var i = 0; i <= limit; i++) { 
              Calc.prototype.doSum = function (limit) {
                 var sum = 0; 

                 for (var i = 0; i <= limit; i++) { 
                    sum = sum + i; 
                    return sum; 
                    return Calc; 
                    TutorialPoint.Calc = Calc; 
                 })(TutorialPoint || (TutorialPoint = {})); 
                 var test = new TutorialPoint.Calc();
              }
           }
        }
     }
  }  
  ```
