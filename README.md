# Javascript Fundamentals [![Awesome](https://cdn.rawgit.com/sindresorhus/awesome/d7305f38d29fed78fa85652e3a63e154dd8e8829/media/badge.svg)](https://github.com/cpandya231/javascript-fundamentals)

This project will provide fundamental concepts of Javascript. This will be one shop stop to get the basics right and also work as a flashcards.

 * [Hoisting](#hoisting)
 * [let vs var](#let-vs-var)
 * [CallStack](#callstack)
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
```
#### <span style="color:blue; font-weight:bold">Output</span>
```
undefined
```

* Keep in mind that window object has 'name' property. So we can use 'name' without assigning/declaring it. In this case we won't get udefined.
* As mentioned before all values var, let, const, function and class are hoisted.

[Reference](https://developer.mozilla.org/en-US/docs/Glossary/Hoisting)

 ## let vs var

* var supports function level scope, let supports block level scope
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

* Keep in mind that, variables declared without any keywords such as 'var' or 'let' will be available from Global scope.

#### Example
```
function setGlobalVariable(){
  globalData="Accessible everywhere";
}
setGlobalVariable();
console.log(globalData);

```

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
### Temporal Dead Zones

* Variables are said to be in Temporal Dead Zones until their definition is evaluated.
  For example, variables declared with 'let' will be in TDZ untill a value is assigned to them.(Same applies for const )<br/> <br/>
* On the contrary, variables declared with 'var' will have default value 'unassigned' until value is assigned to them. They won't be in TDZ.


 ## CallStack
* Javascript interpreter keeps track of all functions invocations.
* Whenever a function is invoked, it is added to the <span style="color:blue; font-weight:bold">CallStack</span>
* If this function again calls for nested function those will be added as well with high precedence.
* Once this function execution is complete they will be taken out of CallStack

 ## IIFE
* Immedietly invoked function expression
* Expression contains two segments:
  1. Anonymous function enclosed with grouping operator <span style="color:red;">( )</span>
  2. Calls the anonymous with second ( )
#### Example
```
let data = { "name": "Chintan" };
(function () {
    console.log(`Data: ${JSON.stringify(data)}`);
})();
```
#### <span style="color:blue; font-weight:bold">Output</span>
```
Data: {"name":"Abc"}
```

 ## Scope
* Scope limits a variable's ability to do stuff.
* 2 types of scopes
  * Local
  * Global

#### Local Scope:
* Variables declared in functions are called local scope variables
* We can not access these variables out side of function.
* Local variable can also be divided into two parts:
  1. Function level
      - As mentioned above, var keywords are function level scoped.
      ##### Example
      ```
      function logName() {
          var name = 'Chintan';

          console.log(name); // logs 'Chintan'

      }

      logName();

      ```
  2. Block level
     - let and const keywords are block level scoped

      ##### Example with 'let'
      ```
      function logName() {
          let showName=true;
         
          if(showName){
            let name = 'Chintan'; 
          }

          console.log(name); //ReferenceError: name is not defined
      }

      logName();
      ```
      * This means that variables declared with let can not be accessed outside of a block.

      ##### Example with 'var'
      ```
      function logName() {
          let showName=true;
         
          if(showName){
            var name = 'Chintan'; 
          }

          console.log(name); //Chintan
      }

      logName();

      ```

#### Global Scope:

* Variable declared outside of function are globally scoped variables.
#### Example
```
var name = 'Chintan';

console.log(name); // logs 'Chintan'

function logName() {
    console.log(name); // 'name' is accessible here and everywhere else
}

logName();
```

## Closure
*Host the JavaScript libraries and provide tools for fetching and packaging them.*

## Context
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

#### Call

* To attach object to 'this' object of a function using call:
```
var car1 = { 
    registrationNumber: "GA12345",
    brand: "Toyota"
}

displayCarDetails.call(car1,"Chintan");

```
* First parameter of call is the object you want to assign to 'this' and all next values will be passed as arguments to the function.

#### Apply

* Same as call method but arguments will be passed as an array :
```
var car2 = { 
    registrationNumber: "GA12345",
    brand: "Tesla"
}

displayCarDetails.apply(car2,["Chintan"]);

```

#### Bind

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

 ## Callback
*Host the JavaScript libraries and provide tools for fetching and packaging them.*

 ## Promise and Async Await
*Host the JavaScript libraries and provide tools for fetching and packaging them.*



