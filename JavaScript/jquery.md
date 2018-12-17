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
