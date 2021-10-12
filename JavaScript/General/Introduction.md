# Introduction

JavaScript is an object-oriented scripting language used to make webpages interactive (Ex: having complex animations, clickable buttons, popup menus)

There are also more advanced server side versions of JavaScript such as Node.js which allow to add more functionality to a website.

### Client Side  JS

Client side JS extends the core language by supplying objects to control a browser and its Document Object Model (DOM). Ex: Client-side extensions allow an application to place elements on an HTML form and respond to user events such as mouse clicks, form input, and page navigation

### Server Side JS

Server side JS extends the core language by supplying objects relevant to running JS on a server. Ex: server-side extensions allow an application to communicate with a database, provide continuity of information from one invocation to another of the application, or perform file manipulations on a server

### Immediately Invoked Function Expression (IIFE)

An IIFE is a function that runs as soon as it is defined. It is a design pattern that is also known as a Self-Executing Anonymous Function

```javascript
(function (name) {
    console.log(name)
})("Test");
```

#### Benefits of IIFE

* Obtaining data privacy 
* Avoiding cluttering the global scope
* Avoid creating a function which takes up a name in the global namespace and increases the possibility of name collisions
* Prevent code snippets executed in the console from interfering with one-another

## Declarations

### Variable Types

JS has 3 types of declarations:

#### `var`

Declares a variable, optionally initializing it to a value

#### `let` 

Declares a block-scoped, local variable, optionally initializing it to a blue

#### `const`

Declares a block-scoped, read-only named constant

### Block Scopes

Code in a block scope is code that is within curly brackets. 

A variable declared using`var` can exist outside a block scope, while a variable declared using `let` cannot

```javascript
function foo(flag) {
    a = 10;
    if(flag) {
        var a = 20;
        console.log(a);
    }
}
function foo2(flag) {
    if(flag) {
        let a = 10;
    }
    console.log(a);
}
foo(false); // 10
foo(true); // 20
foo2(true); // ReferenceError: a is not defined
```

### Destructing Assignment

The destructing assignment syntax makes it possible to unpack values from arrays, or properties from objects, into distinct variables

#### Array Destructuring

```javascript
var [a,b] = [1,2]
```

##### With Default Values

```javascript
var[a=1,b=2] = [3,4]
```

##### Assigning Rest of Array

```javascript
var [a, ...b] = [1,2,3]
// a = 1
// b = [2,3]
```

#### Object Destructuring

```javascript
var user = {name: "user", age=18}
var {name, age} = user
```

##### Assigning to New Variable Names

```javascript
var o = {a: 42, b: true}
var {a: c, b: d} = o
```

##### Default Values

```javascript
var {a = 10, b = 5} = {a=3}
```

##### Assigning New Variable Names with Default Values

```javascript
var {a: aa = 10, b: bb = 5} = {a: 3}
// aa = 3
// bb = 5
```

## Statements

### Label Statement

A `label` provides a statement with an identifier that lets you refer to it elsewhere in the program. 

```javascript
markLoop:
while (theMark == true) {
    doSomething();
}
```

Labels are useful when doing nested loops because then when using a `break` or `continue` statement, you could specify which loop to apply these operations on by putting the name of the label

```javascript
loop1:
	while(true) {
        var x = 1;
        var z = 1;
        x++;
        loop2:
            while(true) {
                z++;
                if(z === 10 && x === 10) {
                    break loop1;
                }
            }
    }
```

### Break Statement

Break statements can be used to terminate `while`,`do-while`,`for`, or `switch`. They can also break labels.

```javascript
break;
break [label];
```

### Continue Statement

Continue statements can be used to restart a `while`,`do-while`,`for`, or `label` statement. In a while loop, it jumps back to the condition. In a for loop, it jumps to the increment expression. If applied to a label, it applies to the looping statement identified with that label.

```javascript
let i = 0;
let n = 0;
while (i < 5) {
  i++;
  if (i === 3) {
    continue;
  }
  n += i;
  console.log(n);
}
//1,3,7,12

let i = 0;
let n = 0;
while (i < 5) {
  i++;
  if (i === 3) {
     // continue;
  }
  n += i;
  console.log(n);
}
// 1,3,6,10,15
```

### for .. in statement

Iterates a specified variable over all the enumerable properties of an object. 

However, it should not be used with array elements, because it will only return the name of user-defined properties in addition to the numeric indexes.

```javascript
car = {make: "Ford", model: "Mustang"};
for (let i in car) {
    console.log(i); // make model
    console.log(car[i]); // Ford Mustang
}
// With Arrays
arr = [1, 2, 3];
arr.foo = "hello";
for (let i in arr) {
    console.log(i); // "0", "1", "2", "foo"
}
```

### for ... of statement

Creates a loop iterating over `iterable objects` (Array, Map, Set, arguments object).

```javascript
arr = [1,2,3]
for (let i of arr) {
    console.log(i); // 1, 2, 3
}
```







