# javascript101
> javascript for noobs

## Execution Context

When you run Javascript, an **Execution Context** is created in the global context and you get the following:
- Global Object (window)
- 'this'
- Outer Environment
- Hoisting (variable and function setup) --> Your Code

In the browser, the **Global Object** is **Window** -- which also happens to be **this**.

In Javascript, **Global** basically means "Not inside a function" 

When the Execution Context is created (Creation Phase) before your code is executed line by line:
Global Object, 'this', are created in memory followed by the setup of memory space for all the variables and functions found in your code - aka "**Hoisting**"
- The entire function and the code inside is set into memory
- Variable assignment is not set in memory (var a = 'alpha';) Instead, **undefined** is assigned to the variable.

Javascript is: 
- Single threaded 
- Synchronous

### Function Invocation and Execution Stack
*Invocation*: Running a function. In Javascript, you invoke a function by using parenthesis()

Steps
1. Global Execution Context is created and code is executed
2. When a function is invoked, a new Execution Context is created then executed into the Execution Stack and the most top is the one currently running
3. Once function is finished invoking, it's popped off the Execution Stack


Readme formatted using github's [markdown](https://help.github.com/articles/basic-writing-and-formatting-syntax/).