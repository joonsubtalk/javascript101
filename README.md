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
- Global Execution Context is created and code is executed
- When a function is invoked, a new Execution Context is created then executed into the Execution Stack and the most top is the one currently running
- Once function is finished invoking, it's popped off the Execution Stack

*Variable Environment*: Where the variables live and how they relate to each other in memory
Each execution context will have its own variable environment.

### Scope Chain
*Scope*: Where a variable is available in the code. If you know scope, you can find out if the variable is the same or a new copy.
Every Execution Context has a reference to its *Outer Environment* -> Lexical Environment (where it is in code) (Not to be confused with Execution Stack)
```
function a(){
	var foo = 'fooey';
	b();
}
function b(){
	console.log(foo); // outputs 'bar' because function b's outer environment is global object
}

var foo = 'bar';
a();
```

### Javascript Engine
- Execution Context Stack (functions being created and executed)
- Event Queue (Clicks, HTTP Requests);doesn't run until execution stack is empty

Once the Execution Context Stack is empty, the *Event Queue* is periodically looked at. If something needs to be run in the Queue, then the execution context is added to the stack and run.

## Types and Javascript


Readme formatted using github's [markdown](https://help.github.com/articles/basic-writing-and-formatting-syntax/).