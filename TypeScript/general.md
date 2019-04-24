# TypeScript

## General

- [Introducing TypeScript](https://channel9.msdn.com/posts/Anders-Hejlsberg-Introducing-TypeScript)

- TypeScript is a superset of JavaScript that implements static-type checking, classes, and interfaces
  - Common errors can be checked for while typing, before compilation
  - Useful for large codebase with multiple developers
  - Open source
  
- TypeScript offers flexible options
  - Any browser
  - Any Host
  - Any OS
  - Tool support (IDEs)

- Key Features
  - Supports standard JS code
  - Provides static typing
  - Encapsulation through classes and modules
  - Support for constructors, properties, and functions
  - Define interfaces
  - ES6
  - Intellisense and syntax checking
    - Supported by IDEs that specifically support TypeScript (e.g. IntelliJ, Visual Studio Code)

- TypeScript Compiler
  - Pass ts file through a TypeScript compiler (tsc)
    - Only for tools that don't support compiler directly
  - Outputs standard JS
  - e.g.
    - TypeScript
    ```js
    class Greeter {
      greeting: string;
      constructor (message: string) {
        this.greeting = message;
      }
      greet() {
        return "Hello, " + this.greeting;
      }
    }
    ```
    - JavaScript
    ```js
    var Greeter = (function () {
      function Greeter(message) {
        this.greeting = message;
      }
      Greeter.prototype.greeter = function () {
        return "Hello, " + this.greeting;
      };
      return Greeter;
    })();
    ```
    
## TypeScript Syntax, Keywords, and Code Hierarchy
  
- Syntax Rules
  - TypeScript is a superset of JavaScript
  - Follows the same syntax rules:
    - {} brackets define code blocks
    - Semi-colons end code expressions
  - JavaScript keywords
    - for
    - if
    - More...
    
- Important Keywords and Operators
  - **class**: Container for members such as properties and functions
  - **constructor**: Provides initialization functionality in a class
  - **exports**: Export a member from a module
  - **extends**: Extends a class or interface
  - **implements**: Implement an interface
  - **imports**: Import a module
  - **interface**: Defines code contract that can be implemented by types
  - **module/namespace**: Container for classes and other code
  - **public/private**: Member visibility modifiers
  - **...**: Rest parameter syntax
  - **=>**: Arrow syntax used with definitions and functions
  - **typename**: <> characters use to cast/convert between types
  - **:**: Separator between variable/parameter names and types

- Code Hierarchy
  - Module/Namespace
    - Interface
    - Class
      - Fields
      - Constructor
      - Properties
      - Functions
