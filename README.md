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

Readme formatted using github's [markdown](https://help.github.com/articles/basic-writing-and-formatting-syntax/).