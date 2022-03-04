# Functions

The definition of a function in JS is: 

```javascript
function func(par) {
    return par;
}
```

## Function Expressions

The function keyword can be used to define a inside an expression. Doing so allows the function name to be omitted, hence creating an **anonymous** function. `myFunc()`

```javascript
const square = function(num) { return num * num; }
console.log(square(4)); // 16
```

A name can also be provided however, which would allow the function to refer to itself (for functional programming) as well as to identify the function in a debugger.

```javascript
const factorial = function fac(n) { return n < 2 ? 1 : n * fac(n-1) }
```

Function expressions can be passed into other functions as arguments. In this example, the contents of an array are multiplied by 2 using a function expression

```javascript
const f = function(x) { return x * 2 }
function multiplyByTwo(func, arr) {
    for (let i = 0; i < arr.length; i++) {
        arr[i] = f(arr[i]);
    }
}
let arr = [1,2,3];
console.log(multiplyByTwo(f, arr)); // 2, 4, 6
```

## Scope and Function Stack

### Function Scope

Variables defined inside a function cannot be accessed from anywhere outside the function/ A function can access all variables and functions defined inside the scope in which it is defined.

A nested function can access all the variables declared within its parent function as well as variables which its parent function has access to

### Recursion

Recursion refers to when a function calls itself. The ways in which a function can call itself are:

1. The function's name
2. `arguments.callee()`
3. An in-scope variable that refers to the function

```javascript
var foo = function bar() {
    foo()
    arguments.callee()
    bar()
}
```

## Closures

A closure is an expression (commonly a function) that can have free variables together with an environment that binds those variables (like closes the expression)

Nested functions are a closure because they inherit the arguments and variables of their containing function. However, the containing function cannot access the variables and arguments of the inner function.

The inner function is only private to the outer function, and can only be accessed within the scope of the outer function.

#### Passing arguments for inner function outside of outer function

Since the inner function forms a closure, the outer function can be called while specifying arguments for both the outer and inner function.

**Note:** Values returned by the inner function will return to the outer function. In order to return them to the function call, the outer function must return them.

```javascript
function outer(x) {
    function inner(y) {
        return x + y;
    }
    return inner;
}
var inside = outer(1);
var outsode = inside(2); // 3
var result = outer(1)(2); // 3
```

### Name Conflicts

When two arguments or variables in the scopes of a closure have the same name, then the the most nested scopes take precedence. 

```javascript
function outer() {
    var x = 5;
    function inmer(x) {
        return x;
    }
    return inner;
}
outer()(2); // 2
```

### Variable Access

Since the inner function has access to the scope of the outer function, the variables and functions defined in the outer function will live loner than the duration of the outer function execution as long as the inner function loves longer than the outer function,

```javascript
var createPet = function(name) {
    var age = 10;
    return {
        var getName = function() {
            return name;
        }
        var getAge = function() {
            return age;
        }
        var setAge(num) {
            age = num;
        }
	}
}
var pet = createPet("Bob");
pet.getName(); // Bob
pet.getAge(); // 10
pet.setAge(5);
pet.getAge(); // 5
```

## Parameters

### Parameter Defaults

Parameters by default are set to `undefined`.There are generally two methods to set the default value of a parameter:

#### Without Default Parameters (Manual Check)

```javascript
function func(a) {
    a = typeof a !== 'undefined' ? a : 1;
}
```

#### With Default Parameters

```javascript
function func(a = 1) {
    return a;
}
```

### Rest Parameters

The rest parameter syntax represents an indefinite number of arguments as an array

```javascript
function multiply(multiplier, ...args) {
    return args.map(x => multipler * x); // Multiplies all the values in args by the multipler
}
multiply(2, 1, 2, 3); // [2, 4, 6]
```

### Arguments Object

The arguments of a function are maintained in an array-like object which can be addressed as `arguments[i]`

With the arguments object, a function can be called with more arguments than it is declared with. `arguments.length` can be used to determine the number of arguments passed.

```javascript
function concatinate(seperator) {
    var result = '';
    for(let i = 1; i < arguments.length; i++) {
        results += arguments[i] + seperator;
    }
    return result;
}
concatinate(',', 'red', 'orange', 'blue'); // red, orange, blue,
```

## Arrow Functions

Arrow functions are compact alternatives to function expressions but with some differences and limitations

* Do not have their own bindings to `this` or `super`, and should not be used as `methods`
* Do not have arguments
* Not suitable for `call`, `apply` and `bind` methods, which generally rely on establishing a scope
* Can not be used as constructors
* Can not use yield within its body

```javascript
// Single Parameter
param => expression
// Multiple Parameters
(param1, param2) => expression
// Multiline statements
param => {
    // Require body brackets and return
}
```

#### Traditional vs Arrow Function

```javascript
// Traditional Function
function (a) {
    return a + 100;
}
// Arrow Function
a => a + 100;

// Multiline Traditional Function
function (a, b) {
    let c = 10;
    return a + b + c;
}

// Multiline Arrow Function
(a, b) => {
    let c = 10;
    return a + b + c;
}
```

### Syntax

#### Named Arrow Functions

```javascript
let func = a => a + 10;
```

#### Returning objects

Returning object literal expressions requires parentheses around expression

```javascript
params => ({foo: 1})
```









