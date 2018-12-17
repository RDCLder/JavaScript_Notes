# jQuery

## General

- jQuery is a DOM manipulation library
  - Utility
    - Select, manipulate, and create elements
    - Add event listeners
    - Add animations and effects
    - Make HTTP Requests (AJAX)
  - Reasons to use
    - Fixes "broken" DOM API (now fixed)
    - Brevity, clarity, and ease of use
    - Cross-browser support
    - Simplifies AJAX
    - Very popular library
  - Reasons to not use
    - DOM API is no longer "broken"
    - Doesn't add additional functionality (everything can be done with normal DOM)
    - Can be an unnecesssary dependancy
      - If you're only using jQuery for a few tasks, there's no need to use jQuery because jQuery provides numerous other features
      - More focused tools (e.g. just for animation) can be more appropriate
    - Performance
    - People are moving away from jQuery
  - Either way, it's worth knowing
  
- Initiation
  - jQuery is essentially a file
    - It can be stored as a local file and referenced in the HTML file
    - It can be linked through a content-distributed network (CDN)
      ```html
      <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
      ```
  - jQuery must be initiated with the following function:
    ```javascript
    // ES5

    $(document).ready(function () {
      //code block
    });

    // ES6

    $(function() {
      // code block
    });
      ```
    - This is equivalent to using ```document.```
    
- Element selection
  - jQuery will return all matching elements in an array
  - Syntax:
    ```js
    // By Tag
    let $tagVar = $("tagName");
    
    // By Class
    let $tagVar = $(".className");
    
    // By ID
    let $tagVar = $("#id");
    
    // Element Inside a List
    let $tagVar = $("li element");
    ```
    - Variable names must be initiated with a ```$```
    - Nested elements can be retrieved by selecting elements sequentially from parent to child
    
  - Examples
    ```js
    let $tagElement = $("img"); // This selects all <img> tags
    
    let $classElement = $(".col"); // This selects all elements with a .col class
    
    let $idElement = $("#myId"); // This selects all elements with a #myId id.
    ```
    ```js
    let $nestedElement = ("ul li a")l
    // This selects all elements that are contained in a list element contained in an unordered list
    // A <a> element that is not in a list will not be selected
    ```
    
- Applying CSS
  - Once an element is selected, it can be manipulated with additional nodes that extend from the base node.
    - ```.css``` is a method that applies css styling to the parent.
  - Syntax
    ```js
    parent.css("property", "value")
    
    // OR
    
    var cssObject = {
      property: "value"
    }
    
    parent.css(cssObject)
    ```
    
  - Example
    ```js
    // Single property argument
    $(#special).css("border", "2px solid red");
    
    // Object argument
    var styles = {
      backgroundColor: "pink",
      height: "50px"
    };
    
    $(#special).css(styles);
    ```

---

## Common Methods

- Most methods use the "getter and setter" paradigm.
  - Leaving the argument blank will return the values of matching elements.
  - Providing an argument will set the values of matching elements to that of the argument.

- **.text()**
  - Utility
    - Get the combined text contents of all matched elements, including their descendants.
    - Set the text contents of every matched element.
  - Syntax:  ```element.text(argument)```
    - Leaving the argument blank will return all the text enclosed by the matching element(s) (including nested elements).
    - Providing a string argument will replace all the text content of the matching element(s) with the string.
  - Examples
    ```html
    <div class="demo-container">
      <div class="demo-box">Demonstration Box</div>
      <ul>
        <li>list item 1</li>
        <li>list <strong>item</strong> 2</li>
      </ul>
    </div>
    ```
    ```js
    $( "div.demo-container" ).text() // Returns: Demonstration Box list item 1 list item 2
    ```
    
- **.html()**
  - Utility
    - Get the HTML contents of the first element in the set of matched elements.
    - Set the HTML contents of every matched element.
  - Syntax: ```element.html(argument)```
    - Leaving the argument blank will return the HTML content of the first matched element.
    - Providing an argument will replace all HTML content of all matched elements.
  - Examples
    ```html
    <div class="demo-container">
      <div class="demo-box">Demonstration Box</div>
    </div>
    ```
    ```js
    $( "div.demo-container" ).html(); // Returns:
    ```
    ```html
    <div class="demo-box">Demonstration Box</div>
    ```
    ```js
    $( "div.demo-container" ).html( "<p>All new content. <em>You bet!</em></p>" );
    // Returns:
    ```
    ```html
    <div class="demo-container">
      <p>All new content. <em>You bet!</em></p>
    </div>
    ```
    
- **.attr()**
  - Utility
    - Get the value of a specified attribute for the first element in the set of matched elements.
    - Set one or more attributes for every matched element.
  - Syntax: ```element.attr(attribute, value)```
    - Attribute values are usually strings with the exception of a few attributes (e.g. value, tabindex)
    - Leaving the argument blank will return the specified attribute value for all matching elements.
    - Providing an argument will replace all specified attribute values for all matched elements.
  - **.attr()** vs. **.prop()**
    - **.prop()** retrieves attributes that can have any type of value (e.g. numbers, booleans, objects, etc.)
    - Most attributes/properties are interchangeable though
  - Examples
    ```html
    <img id="greatphoto" src="brush-seller.jpg" alt="brush seller">
    ```
    ```js
    $( "#greatphoto" ).attr( "alt", "Beijing Brush Seller" ); // This replaces "alt" value to "Beijing Brush Seller"
    ```
    
- **.val()**
  - Utility
    - Primarily used for form elements such as ```input```, ```select```, and ```textarea```.
    - Get the current value of the first element in the set of matched elements.
    - Set the value of every matched element.
  - Syntax: ```element.val(argument)
    - Leaving the argument blank will return the value for all matching elements.
    - Providing an argument will replace the values for all matched elements.
  - Examples
  
