# Principles of JavaScript

## Execution Context

- JavaScript is single-threaded so it can only do one thing at once.

- Execution Context
  - Kepps track of where the thread is executing
  - Default context is global
  - A new local context is created whenever a function is called

- When a program is executed, the call stack keeps track of
  - The execution context, global or local
  - The current context is always at the top of the stack
  - Changing a context will push the new context to the top of the stack

- Execution context stores everything in a data structure called a stack
  - "Last in, first out"
  
- Variable Environment
  - Variables are stored in the scope they exist in
  
## Functional Programming

- Functional programming is a paradigm for programming at scale
