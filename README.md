# Javascript Fundamentals [![Awesome](https://cdn.rawgit.com/sindresorhus/awesome/d7305f38d29fed78fa85652e3a63e154dd8e8829/media/badge.svg)](https://github.com/cpandya231/javascript-fundamentals)

This project will provide fundamental concepts of Javascript. This will be one shop stop to get the basics right and also work as a flashcards.

 * [Hoisting](#hoisting)
 * [let vs var](#let-vs-var)
 * [Callstack](#callstack)
 * [IIFE](#iife)
 * [Scope](#scope)
 * [Callback](#callback)
 * [Promise and Async Await](#promise-and-async-await)
 * [Call Apply and Bind](#call-apply-and-bind)
 
 
 ## Hoisting

* Conceptually, Javascript moves all variables, functions, class to the top of the code. This is called Hoisting.
* Javascript does not reshuffle any code but at compile time it identifies variable, function declaration first. Variable assignment happens at later stage.

#### Example
```
var myName;
console.log(myName);
myName = ‘Sunil’;

Result:
udenfined
```
* Keep in mind that window object has 'name' property. So we can use 'name' without assigning/declaring it. In this case we won't get udefined.
* As mentioned before all values var, let, const, function and class are hoisted.

* [Reference](https://developer.mozilla.org/en-US/docs/Glossary/Hoisting)

 ## let vs var

* var is function scope, let is block scope
#### Example
```
'use strict';
function varTest() {
  var x = 1;
  {
    var x = 2;  // same variable!
    console.log(x);  // 2
  }
  console.log(x);  // 2
}

function letTest() {
  let x = 1;
  {
    let x = 2;  // different variable
    console.log(x);  // 2
  }
  console.log(x);  // 1
}

```

* If you create a var at the top level (global level), it would create a property on the global object — in the case of a browser, this is likely to be the window object. So creating var myName = 'Chintan'; can also be referenced by calling window.myName. This will not happen in case of let(it will give undefined).
* In strict mode, var will let you re-declare the same variable in the same scope while let raises a SyntaxError.
#### Example
```
'use strict';
var foo = "foo1";
var foo = "foo2"; // No problem, 'foo' is replaced.

let bar = "bar1";
let bar = "bar2"; //Error

```
* 'var' is initialized with 'undefined'. 'let' is not initialized until it is declared. In this case 'let' will be there in 'temporal dead zone'

```
function do_something() {
  console.log(bar); // undefined
  console.log(foo); // ReferenceError
  var bar = 1;
  let foo = 2;
}

```
## Temporal Dead Zones

 ## Callstack
*Host the JavaScript libraries and provide tools for fetching and packaging them.*

 ## IIFE
*Host the JavaScript libraries and provide tools for fetching and packaging them.*

 ## Scope
*Host the JavaScript libraries and provide tools for fetching and packaging them.*

 ## Callback
*Host the JavaScript libraries and provide tools for fetching and packaging them.*

 ## Promise and Async Await
*Host the JavaScript libraries and provide tools for fetching and packaging them.*

## Call Apply and Bind
* All of these method belong to Function.prototype property.
* These methods can be used to apply 'this' object to the function.
* Initial setup:
```
function displayCarDetails(ownerName) {
  console.log(ownerName + ", this is your car: " + this.registrationNumber + " " + this.brand);
}

```
* Since function is also an object, we can assign json object to the function's 'this' object.

### Call

* To attach object to 'this' object of a function using call:
```
var car1 = { 
    registrationNumber: "GA12345",
    brand: "Toyota"
}

displayCarDetails.call(car1,"Chintan");

```
* First parameter of call is the object you want to assign to 'this' and all next values will be passed as arguments to the function.

### Apply

* Same as call method but arguments will be passed as an array :
```
var car2 = { 
    registrationNumber: "GA12345",
    brand: "Tesla"
}

displayCarDetails.apply(car2,["Chintan"]);

```

### Bind

* Only difference between call and bind is that bind returns a function with the object we attached to 'this'. Bind does not call the function.
```
var car3 = { 
    registrationNumber: "GA12345",
    brand: "BMW"
}

var bindFunction=displayCarDetails.bind(car3,"Chintan");

bindFunction();

or

var bindFunction=displayCarDetails.bind(car3);

bindFunction("Chintan");


```




