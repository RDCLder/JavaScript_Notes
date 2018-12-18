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
      <script
        src="https://code.jquery.com/jquery-3.3.1.min.js"
        integrity="sha256-FgpCb/KJQlLNfOu91ta32o/NMZxltwRo8QtmkMRdAu8="
        crossorigin="anonymous">
      </script>
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

- Creating Elements
  - Syntax
    - General
      ```var $elementName = $(<tag>);```
      - jQuery elements must always be initiated with a ```$``` symbol.
    - With Attributes
      ```var $elementName = $(<tag>, {
        "key": "value"
      });```
      - Object syntax is used.
  - Examples
    ```js
    var $anchor = $('<a>', {
      'class': 'nav-item',
      'data-image': 'trigger',
      'text': 'Click me!'
    });
    ```

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
    ```js
    $("input").val(""); // Resets everything in the input field to an empty string
    ```

- **.addClass()** & **.removeClass()**
  - Utility:  Add a specified class to each matching element.
  - Syntax:  ```element.addClass(className)``` & ```element.removeClass(className)```
    - Multiple classes can be added/removed in the same argument by separating each className with a space
      ```element.addClass(class1 class2 class3)```

- **.toggleClass()**
  - Utility:  Either add or removed the specified class to each matching element if the class was present/missing, respectively.
  - Syntax:  ```element.toggleClass(className)```
    - Multiple classes can be input in the same argument.
  - Example
    ```html
    <div class="tumble bounce">Some text.</div>
    ```
    ```js
    $("div").toggleClass("tumble"); // This removes the "tumble" class
    $("div").toggleClass("hop"); // This adds the "hop" class
    ```

- **.append()**
  - Utility:  Insert content, specified by the parameter, to the end of each matching element.
  - Syntax:  ```element.append(content)```
    - Content can include HTML to both create an element and append it in the same statement.
    - Multiple arguments can be passed 
  - Examples
    ```html
    <h2>Greetings</h2>
    <div class="container">
      <div class="inner">Hello</div>
      <div class="inner">Goodbye</div>
    </div>
    ```
    ```js
    $(".inner" ).append( "<p>Test</p>");
    // This inserts the enclosed <p> element into the two .inner elements.
    ```
    ```html
    <h2>Greetings</h2>
    <div class="container">
      <div class="inner">
        Hello
        <p>Test</p>
      </div>
      <div class="inner">
        Goodbye
        <p>Test</p>
      </div>
    </div>
    ```

---

## Events

- **.click()**
  - Utility:  Add a click listener to matching elements.
  - Syntax: ```element.click(function)```
    - Can be used with any element.
  - Example
    ```html
    <button>Click Me</button>
    ```
    ```js
    $("button").click(() => {
      alert("You clicked me!");
      $(this).css("background", "red");
    });
    ```
    - ```$(this)``` corresponds to the element to which the event listener is attached.

- **.keypress()**, **.keydown()**, & **.keyup()**
  - Utility:  Adds a keypress listener to matching elements.
    - **.keypress()**:  Adds the listener to the middle of the keystroke between pressing down and releasing.
    - **.keydown()**:  Adds the listener to the moment a key is pressed down.
    - **.keyup()**:  Adds the listener to the moment after a key is released.
  - Syntax: ```element.keypress(handler)```
    - **.keypress()** only processes the character while the other two methods process the key itself
  - Example
    ```html
    <form>
      <fieldset>
        <input id="target" type="text" value="Hello there">
      </fieldset>
    </form>
    <div id="other">
      Trigger the handler
    </div>
    ```
    ```js
    $('input[type = "text"]').keypress(function(){
      alert("text input keypress!"); // This triggers the alert everytime a key is pressed when entering the input
    });
    ```

- **.on()**
  - Utility:  Adds an event listener for a specified event type.
    - Other event listeners are only added for existing elements.
    - **.on()** adds event listeners for all future elements as well.
  - Syntax:  ```element.on("eventType", function)```
  - Examples
    ```js
    // Click Event
    $("submit").on("click", function() {
      console.log("Another click"); // This logs a message anytime a button is clicked.
    });
    
    // Keypress Event
    $('input[type="text"]').on("keypress", function() {
      alert("Key press in an input!");
    });
    ```

---

## Effects

- **.fadeOut(), .fadeIn(), & .fadeToggle()**
  - Utility
    - **.fadeOut()**:  Fade the matching elements to transparent
    - **.fadeIn()**:  Transform the matching elements from transparent to visible
    - **.fadeToggle()**:  Transform the matching element to opposite of starting state
  - Syntax:  ```element.fadeOut(duration, easing, complete)```
    - ```duration```:  Number or string which determines how long the effect lasts (default is 4000 ms)
    - ```easing```:  Type of effect to be used
    - ```complete```:  Function to call when effect is complete (optional)
  - Example
  ```html
  <div id="clickme">
    Click here
  </div>
  <img id="book" src="book.png" alt="" width="100" height="123">
  ```
  ```js
  $( "#clickme" ).click(function() {
    $( "#book" ).fadeOut( "slow", function() {
      // Animation complete.
    });
  });
  ```
  
- **.slideDown(), .slideUp(), & .slideToggle()**
  - Utility:  Display the matching elements with a sliding motion up or down
  - Syntax:  ```element.slideDown(duration, options, complete)```
    - ```duration```:  Number or string determining how long the effect lasts (default is 4000 ms)
    - ```options```:  Different optional effects to run
    - ```complete```:  Function to run once the animation is completed (optional)
  - Examples
  ```html
  <div id="clickme">
    Click here
  </div>
  <img id="book" src="book.png" alt="" width="100" height="123">
  ```
  ```js
  $( "#clickme" ).click(function() {
    $( "#book" ).slideDown( "slow", function() {
      // Animation complete.
    });
  });
  ```
