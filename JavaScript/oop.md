# Object-Oriented Programming

## Advanced Objects

- Objects can be created in several ways
  - Literal Notation
    - Creates an empty object
    - Syntax: ```var objectName = {};```
  - Object Constructor Notation
    - ```new``` keyword and object constructor create an empty object
    - Syntax: ```var objectName = new Object();```
    - e.g.
      - ```var newObject = new Object();```
      - ```var newString = new String();```
      - ```var newNumber = new Number();```
      - ```var newArray = new Array();```
      - ```var newFunction = new Function();```
      - etc.
  
- Object Constructor Method
  - Method to initiate a new object of a specific class
  - Properties or attributes can be accessed with dot notation
    - e.g. ```objectName.value``` accesses the ```value``` property of ```objectName```.
    
- Object Types (Blueprints/Classes)
  - Previous methods only create single instances of a specific object type.
  - An **object type** can be used to initiate objects with specific properties and methods.
  - Object types can be defined with the **object constructor function**.
  
- Object Constructor Function
  - A function that creates a new type of objects (i.e. python class equivalent)
  - Syntax: ```function ObjectTypeName(initialAttributes) {}```
  - e.g.
    ```javascript
    function Course(title, instructor, level, published, views) {
      this.title = title;
      this.instructor = instructor;
      this.level = level;
      this.published = published;
      this.views = views;
    }
    ```
  - Objects of the same type are created by calling the constructor function with the ```new``` keyword.
    - e.g.
      ```javascript
      var Course1 = new Course("DigitalCrafts 16 Week Bootcamp", "Veronica", 1, true, 0);
      ```
      
- Objects as Dictionaries
  - Method 1
    ```javascript
    var objectName = {};
    objectName.item1 = "";
    objectname.item2 = [];
    objectName.item3 = {};
    ```
  - Method 2
    ```javascript
    var objectName = {
      item1: "",
      item2: [],
      item3: {}
    {
    ```
  - Object properties can be accessed in two ways.
    - Dot Notation: ```objectName.propertyName1```
    - Bracket Notation: ```objectName["propertyName"]```
    
- Object Functions/Methods
  - **Delete**: Deletes a specified property from an object.
    - Syntax: ```delete objectName[keyName]```
    - e.g. ```delete Course1["title"]```;
    
- Looping Through Objects
  - General loop syntax can be used.
  - e.g.
    ```javascript
    for (var attribute in person) { // attribute will be equivalent to range(0, person.length)
      var value = person[attribute];
      console.log("${attribute}: ${value}");
    }
    ```

## Prototypes

- JavaScri[t is a prototype-based language and inheritance is based on prototypes.
  - Each object has a prototype object which acts as a template object from which methods and properties are inherited.
    - i.e. The prototype object is a class blueprint that defines initial attributes and methods.
    - Prototype objects can inherit from other prototype objects
