# React.js

- [Documentation](https://reactjs.org/docs/getting-started.html)

## General

- React is an open-source, front-end library for building UI
  - The V in [MVC](https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller)
  - Design simple declarative views for each state in your application
  - Encapsulated Components
  - Dynamic properties & state
  - Virtual DOM
  - Completely independent of the rest of your application
  - Can render on the client or server
  
- Virtual DOM
  - React abstracts away the DOM and creates its own version
    - Simplified and only includes the things that you need
    - Determines how to upload the browser's DOM more efficiently
    - Lightweight and faster than traditional DOM
  - Uses states to identify which parts have changes
  
- Architecture
  - Component manage own State
  - One way binding
  - JSX
  - Virtual DOM
  - Component Lifecycle
  - Model + component = DOM
  
- Dependencies
  - React – the React top level API
    ```html
    <script crossorigin src="https://unpkg.com/react@16/umd/react.development.js"></script>
    ```
  - React DOM – adds DOM-specific methods
    ```html
    <script crossorigin src="https://unpkg.com/react-dom@16/umd/react-dom.development.js"></script>
    ```
  - Babel – a JavaScript compiler that lets us use ES6+ in old browsers
    ```html
    <script src="https://unpkg.com/babel-standalone@6.26.0/babel.js"></script>
    ```

- JSX
  - JavaScript XML
    - Combines HTML and JS
    - Create custom XML tags
  - Not mandatory for React
  - e.g.
    ```js
    // Using JSX
    const heading = <h1 className="site-heading">Hello, React</h1>;
    ```
    ```js
    // Using React
    const heading = React.createElement(
      'h1',
      {className: 'site-heading'},
      'Hello, React!'
    );
    ```
      - Takes element tag, object containing properties, and children of the component

- Components
  - 

## React Methods

- ```React.createElement()```
  - Create and return a new React element of the given type.
    - Typically use JSX
  - e.g.
    ```js
    // DOM
    let h1 = document.createElement('h1');
    ```
    ```js
    // React
    let h1 = React.createElement('h1', null, 'Albums');
    ```
    
- ```ReactDOM.render()```
  - The render method returns a description of what you want to see on the screen.
  - React takes the description and displays the result.
  - In particular, render returns a React element, which is a lightweight description of what to render.
    ```js
    ReactDOM.render(h1, document.getElementById('root'));
    ```
