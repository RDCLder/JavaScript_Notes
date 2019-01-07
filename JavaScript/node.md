# Node.js

## General

- Node.js is an open-source, cross-platform runtime environment used for development of server-side web applications.
  - Node exports Chrome's V8 JavaScript engine combined with some libraries for I/O and networking functionality
    - JavaScript is traditionally only client-side on the browser
    - Node allows for JavaScript to be run on the server-side (e.g local computers) as well.
  - Based on an event-driven architecture & non-blocking I/O API that is designed to optimize an application through output and scalability for real-time web applications
  - The node package ecosystem, npm, is the largest for open source libraries in the world.

- Why use Node
  - Node allows for JavaScript to be run outside of a browser on the server-side (e.g local computers).
  - Handling of Concurrent Requests
    - Asynchronous event-driven I/O helps concurrent request handling
      - If a request is received by Node for some I/O operation, it will execute the operation in the backround and continue with processing other requests.
      - For other languages, an I/O block causes the entire program to wait for the I/O operation to finish first.
    - Capable of handling concurrent connections with minimal overhead on a single process
  - Node is an open-source framework with a large, active community.
  
- When to use Node
  - Node is effective for handling high levels of concurrency and requests that do not require high computation.
    - "Light" I/O requests
  - Examples
    - Chat applications
    - Game servers
    - Collaborative environment
    - Advertisement servers
    - Streaming servers
    
- When to not use Node
  - Node is structured to be single-threaded. If a request requires computation, it slows down the whole thread process.
  - Examples
    - Mathematical calculations
    - Image resizing
    - JSON parsing
    - Regular expressions
