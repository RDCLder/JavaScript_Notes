# Basic HTML

## Objectives

- Write properly structured HTML documents
- Write common closing and self-closing tags
- Recreate a simple website based on a provided photo

---

## General

- Front-end consists of HTML, CSS, and JavaScript (or another scripting language).
  - HTML:  Hypertext Markup Language.  The structure (noun) of a website.
  - CSS:  Cascading Style Sheets.  The styling (adjective) of a website.
  - JavaScript/other:  The behavior (verb) of a website.
  
- HTML General Rule
  - Tags are used to enclose and structure content.
    - Syntax: ```<tagName> Content </tagName>```
    - e.g. ```<h1>This is header text</h1>```

- HTML Boilerplate
  - Code that every HTML document initiates with.
    - Type ```html``` and hit tab
  - Structure
    - HTML
      - The HTML root element.  All other elements must be enclosed by this element.
    - Head
        - Provides general information (metadata) including title of webpage.
        - Includes links/definitions of scripts and style sheets (CSS).
    - Body
      - The contents of the document.

- Common Tags
  - Headers: ```<h1>I'm a header</h1>```
    - Headers range from ```h1``` to ```h6```
  - Paragraph: ```<p>I'm a paragraph</p>```
  - Button: ```<button>I'm a button</>```
  - Lists:
    - Ordered: 
    ```html
    <ul>
      <li>Item 1</li>
      <li>Item 2</li>
    </ul>
    ```
    - Unordered: 
    ```html
    <ul>
      <li>Item 1</li>
      <li>Item 2</li>
    </ul>
    ```
  - Image: ```<img src = "[insert URL/local path]">```
  - Anchor/link: ```<a href = "URL/local path">Display Text</a>```
    - The display text can either be plain text or an object (e.g. image).
    - The link (href value) can either be local through the file protocal or online through http (hypertext transfer protocal).

- <div> & <span> tag
  - ```<div>``` is a block-level generic container.
  - ```<span>``` is an inline-level generic container.
  - Properties
    - Can be modified into any class.
    - Other containers have their own tags (e.g. img, a, ul).

- Attributes
  - Add additional information to tags
  - Syntax: ```<tag name="value"></tag>```
    - ```name``` refers to the attribute name.
  - e.g.
    - ```<img src = "corgi.png">```
    - ```<a href = "google.com">Cick me to go to Google</a>```

---

## Miscellanenous

- Resources
  - [MDN](https://developer.mozilla.org/en-US/docs/Web/HTML): Mozilla Developer Network.
  - [FreeCodeCamp.com](https://www.freecodecamp.org/): Covers full-stack web development.
