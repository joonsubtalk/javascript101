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
- Dynamic Typing

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
*Dynamic Typing* type figured out during execution
*Primitive Types*: Represents a single value; not an object
- undefined
- null
- boolean
- number
- string
- symbol (ES6)

### Operators: (special type of functions)
Infix Notation a+b
Prefix Notaction +a,b
Postfix Notaction a,b+

## Precedence and Associativity [link](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_Precedence)
Left to Right vs Right to Left (dependent on associativity);

## Coercion: Converting a value from one type to another; because Javascript is dynamically typed
NaN: Javascript's way of saying, I have something that I have no way to convert to a number.
=== : Tests for strict equality, by *not* coercing the values.
Coercion comparison table [link](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness)
```
function hello(name) {
	console.log('Hello ' + name);
}
hello(); // Hello undefined
```
Simple fix: Use Coercion to your advantage. The || (OR) operator coerces values
```
function hello2(name){
	name = name || '<Your name here>';
	console.log('Hello '+name);
}
hello(); // Hello <Your name here>
```

## Objects and Functions
An Object can have:
- Primitive: "Property"
- Object: "Property"
- Function: "Method"

```
// There are better ways... Not the preferred way for creating objects, but for clarity...
var person = new Object();

// Adding property and methods
person["firstname"] = "Tony"; // Computed member access
person["lastname"] = "Tiger";

var firstNameProperty = "firstname";

console.log(person);                    // Returns person Object
console.log(person[firstNameProperty]); // "Tony"

// dot operator
console.log(person.firstname)           // "Tony"
console.log(person.lastname)            // "Tiger"

// There's better ways to set a new address Object, but for now...
person.address = new Object();
person.address.street = "123 won st.";
person.address.city = "NY";

console.log(person.address.city);
console.log(person["address"]["city"]);
```

## Object Literals
```
// not preferred way...
var person = new Object();

// short hand:
var person = {};

// we can add name value pairs to the Object Literal:
var person = {
    firstname: "Tony",
    lastname: "Tiger",
    address: {
        street: "123 won st.",
        city: "NY"
    }
}

function greet(person){
    console.log('Hi ' + person.firstname);
}

greet(person);      // Hi Tony

// can create Obj on the fly
greet({
    firstname: "Foo",
    lastname: "Bar"
});

// can add on the fly:
person.middlename = "Billy";
```

*Namespace*: A container for variables and functions: typically to keep variables and functions with the same name separate. JS doesn't natively have namespaces. You can fake it by using a container object.
```
var korean = {
	greet: 'anyong'
}
var english = {
	greet: 'hello'
}
```

## Functions are Objects:

*First class functions:* Everything you can do with other types you can do with functions.
e.g. Assign them to variables, pass them around, create them on the fly.

A Function is simply a special type of an Object.
- It can have a primitive, Object, Function as a property
- In addition, it can have a name (optional); Else, anonymous
- It has a Code property which can be invoked using '()'

*Expression:* Unit of code that results in a value; it doesn't have to save to a variable.
*Statement*: just does work
```
//Expression
var a;
a = 3;	// a unit of code;
1+2; 	// a valid expression; Did not set anything to memory, but returned a value

//Statement
if (a === 3) { // a===3 is an expression. However, this is an if statement.

}

//Function statement
function greet() {		// get's hoisted, but returns nothing.
	console.log('hi');
}

// Function Expression	// They are not hoisted. Only the variable is hoisted.
var anonymousGreet = function(){	// This is an anonymouse function.
	console.log('hi');
}
```

Function Statements: hoisted in memory
Function Expressions: can pass function as a param; because JS uses 1st class function

## By value vs reference
```
// by value
var a = 3;
var b;
b = a;

// by reference; all objects -- including functions
var c = {greet:'sup'};
var d;
d=c; //d is pointing to the same object as c is. It's not a copy of object c.
c.greet = 'hi'; // mutated; d.greet will also be 'hi'
```

*mutate:* to change something
*immutable:* can't be changed

The equal operator sets up new memory space (new address)
```
var c = {greet:'hello'}; // no longer affects object d since they point to a new memory space.
```


## This
Examples of three separate execution contexts, but 'this' still pointing to the same window object
```
console.log(this); // 'this' same as the global window object

function a(){
	console.log(this);
}
a(); //this points again to the window object

var b = function() {
	console.log(this);
}
b(); // this still points to the window object
```

When you just invoke a function, the 'this' variable is still pointing to the global object

```
var c = {
	name: 'The c object',
	log: function(){			// method on an object
		this.name = 'updated c object';		// 'this' points to c object, therefore c.name will change.
		console.log(this);
	}
}
c.log();	// a function attached to an object, this refers to the object that the method resides in.
```

Let's look at an interesting question...

```
var c = {
	name: 'The c object',
	log: function(){
		this.name = 'updated c object';
		console.log(this);

		var setName = function(newName) { // This internal function, when Execution context created, actually points to the global object
			this.name = newName;		// NOTE!!! Actually updates the window global Object
		}
		setName('Updated again!');
		console.log(this);
	}
}
c.log();	// a function attached to an object, this refers to the object that the method resides in.
```

How do you fix 'this'?
Remember that Object are passed as reference in Javascript

set this to a variable

```
var c = {
	name: 'The c object',
	log: function(){
		var m = this;
		m.name = 'updated c object';
		console.log(m);

		var setName = function(newName) {
			m.name = newName;		// Now it changes the c object's name variable.
		}
		setName('Updated again!');
		console.log(m);
	}
}
c.log();	// a function attached to an object, this refers to the object that the method resides in.
```

## Arrays
```
// arrays are dynamically typed; put whatever you want
var arr = [1,'tom',false,{name:'John'}, function(name){var greet = 'hello '; console.log(greet+name);}];
arr[4](arr[3].name); // invoke a function in array
```

## Arguments & spread
'arguments' -- contains list of all the values and all the parameters passed to a function.
**Arguments** : The parameters you pass to a function; Javascript gives you a keyword of the same name which contains them all.

```
function greet(name, language){
	//Slight hack to have default parameters
	language = language || 'en'; // checks if language is undefined (coerced to false), if so, set to 'en';
	console.log(arguments); // not exactly an array, but kinda like an array.

	// arguments.length can tell you how many arguments sent to greet function
	// arguments[0] will give you the first value inside arguments "array"

	// In the new version of Javascript: spread. other is an array that hold all the extra params.
	// function greet(name, language, ...other){}
}

```

## Immediately Invoked Function Expression AKA IIFE
recall that:
```
// statement
function greet() {
	return "hello";
}
//expression
var greeter = function(){
	return "hello";
}

// IIFE
var helloer = function(){
	return "hi!";
}();
// console.log(helloer) // returns "hi!"

// Error -- expects a function statement
function(){
	return "hello";
}

// parenthesis is an operator; only to be used with expressions
(function(){
	return "hello";
}); // valid

// we can do something interesting now...
(function(name){
	console.log("hello " + name);
}('john')); // IIFE to a valid Function expression Immediately invoked.

```

## Closures
Remember lexical scoping! Remember functions have access to outer variables!
```
function greet(whatToSay){
	return function(name){
		console.log(whatToSay + ' ' + name);
	}
}

greet('Hi')('Tony');

var sayHi = greet('Hi');
sayHi('Tony');
```

Typical closure problem:
```
function build(){
 var arr= [];
 for (var i = 0; i < 3; i++){
  arr.push(
   function() {
     console.log(i);
   }
  )
 }
  return arr;
}


var fs = build();
fs[0]();
fs[1]();
fs[2]();
```

Function Factories takes advantage of closure to set a parameter value used inside a function that's returned.

Closure and Callbacks
```
function sayHiLater(){
	var greeting = 'Hi!';
	setTimeout(function(){
		console.log(greeting);
	},2000)
}
```

**Callback Function**: A function you give to another function, to be run when the other function is finished.
So the function you call (i.e. invoke), 'calls back' by calling the function you gave it when it finishes.

```
function callMeWhenDone(callback){
	var a = "do something ";
	var b = 200;
	
	callback();
}

callMeWhenDone(
	function(){
		console.log("I'm a callback");
	}
);
```


Readme formatted using github's [markdown](https://help.github.com/articles/basic-writing-and-formatting-syntax/).
