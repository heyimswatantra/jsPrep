# JS brushUp

## Primitives vs Reference types in JS
- Primitives are number, string, boolean, null and undefined (these store single values)
- Reference types are array, objects and function (these store multiple values) <br> **The key difference is how they are stored in memory**
- primitives are directly stored in variable's location
- while non-primitives store a reference to object in the memory

## Difference between For-of and For-in loop
- for-of provides direct access to values of iterable not indices or keys
- for-in returns keys (property names or indices rather than values) not recommended for arrays becoz of possible case of prototype chain traversal

## First Class Function
- funcs are treated as first class citizens in JS, meaning they can treated as any other value (str, num or obj)
- funcs can be assigned to variables, they can be passed as arg to other funcs and also can be returned as values from other funcs

## Constructor functions
- these are special func in JS used for creating and initializing objects
- they are a way to define blueprint for objects 
- objects can be instantiated with __new__ keyword
```javascript 
    function Preson(name, age){
        this.name = name;
        this.age = age;
        function sayhello(){
            console.log(`Hello my name is ${name}`)
        }
    }

    const billy = new Person("Billy", 25)
    console.log(preson1.name, person1.sayhello());
```

## Arrays as Objects
- arrays are special type of objects that has special __length__ property and methods like __push__, __pop__, __shift__
- arrays use numeric indices to access elements but these indices are actually *converted to strings* and used as **property names** internally

## Different ways to created objects in JS

1. Object literals
```javascript 
    const person = {
        name: "John",
        age: 25,
        sayHello: function(){
            log(name)
        }
    }
```

2. Object constructor
```javascript 
    fucntion person(name, age){
        this.name: name;
        this.age: age;
        function sayHello(){
            log(name);
        }
    }
    const billy = new Person("Billy", 25)
```

3. Object.create() Method
```javascript 
    const personPrototype = {
        sayHello: function(){
            log(name)
        }
    };
    const person = Object.create(personPrototype);
    person.name = "Billy";
    person.age = 25;
```

4. Class Syntax (ES6) 
```javascript 
    class Person {
        constructor(name, age) {
            this.name: name;
            this.age: age;
            function sayHello(){
                log(name);
            }
        }
    }
    const billy = new Person("Billy", 25)
```

5. Function Returning Objects
```javascript 
    function createPerson(name, age) {
        return {
            name: name,
            age: age,
        }
    }
    const person = createPerson("Billy", 25);
```

## How objects in JS are different from objects in other langs
1. Dynamic Typing
- properties can be added or deleted on the fly
```javascript
const myObj = {}
myObj.name = "John"; //adding prop
delete myObj.name; // deleting prop
```

2. Prototypal Inheritance
- inheritance is through prototypes, obj can inherit properties and method from other objs through their prototypes, this is in contrast to classical inheritance found in other langs where classes are defined as blueprint for objs
```javascript
function Person(name) {
    this.name = name;
}
Person.prototype.sayHello = function(){
    log(name);
};
const john = new Person("John");
john.sayHello(); // Outputs: Hello
```

3. Object Notation
- objs are defined using literal notation making obj create consive and expressive
```javascript 
    const person = {
        name: "John",
        age: 25,
        sayHello: function(){
            log(name)
        }
    }
```
4. Lack of Classes (before ES6)

5. Loose Structure
6. Functions as First Class citizens

## How to freeze Objects in JS
- **Object.freeze()** method prevents modifications to an object
- freezing means that you cannot add, remove or modify properties or values of object
> However, Object.freeze() operates at top-level, so if there are nested objects, we may want to use a recursive approach

## Prototype in JS  
Prototype is an object that is associated with every object and serves as a fallback source of properties and method that the object does not have directly.<br>
Each object has link to its prototype called `[[Prototype]]` and can be accessed throught `Object.getPrototypeOf()`

## Prototypal Inheritance
Protypal Inheritance is mechanism by which a object can inherit properties and methods from another object. <br>
This is achieved through prototype chain, when we try access a property or method in the object, JS finds it in ther object itself, and if does not find it, JS looks in the object's prototype and this process continues up the prototype chain until the property/method is found or it has reached end of the chain.

## Lambda functions (Arrow functions)

Lambda functions are concise way to write anonymous fucntions 
```javascript 
const add = (a, b) => a+b
```
- Key characteristics
1. Concise Syntax
2. Implicit Return
3. No _this_ binding
```javascript 
function cntr() {
    this.count = 0;
    setTimeout(function() { // traditional function with this binding
        this.count++;
        console.log(this.count); // logs NaN (losses the context)
    }, 1000);

    setTimeout(() => { // Arrow function with Inherited this
        this.count++;
        console.log(this.count) // works as expected
    }, 1000);
}

const cnt = new cntr();
```

## Pure functions
Functions that give same output for given input and do not modify the external state
```javascript
    function add(a, b) { // Pure function
        return a + b;
    }
    let total = 0;
    function addTotal(val) { // Impure function (has side effect)
        return total += val;
    }
```

## Curring in JS 
Curring is technique of converting a function that takes multiple args into a sequence of functions that takes single arg
```javascript
    function add(a, b){
        return a+b;
    }
    function curryAdd(a) {
        return function(b) {
            return a+b;
        }
    }
    // curring in arrow function
    const curryAdd = a => b => a + b;

    console.log(curryAdd(2)(3)) // logs 5
```
- allows to make our code modular and reusable

## Hoisting 
Hoisting is a behavior in JS  where variable and function declarations are moved to the top of thier containing scope. <br>
This behavior allows to use variables and functions before they are declared in the code.

```javascript 
    console.log(x); // logs undefined instead of error becoz of hoisting
    var x = 7;
    console.log(x); // log 5

    sayHello(); // logs "Hello"
    function sayHello() {
        console.log("Hello");
    }
```
> __Only declarations are hoisted and not initializations__

## Temporal Dead Zone (TDZ)
 TDZ refers to the time span between entering a scope and the point where a variable is declared.
<br>
During temporal dead zone any reference to the variable results in `ReferenceError`
```javascript
console.log(myVar) // logs ReferenceError: Cannot access 'myVar' before initialization
let myVar = 46;
```
This behavior is becoz of `let` and `const` declarations.
<br>
Unlike `var` declarations which are hoisted and initialiazed with `undefined`.
<br>
`let` and `const` declarations are hoisted as well but are not initialized until the actual intialization line occurs.

## IIFE (immediately invoked function expression)
IIFE is a pattern where a function is defined and executed immediately after being created.
<br>
This pattern is often used to created a private scope for variables and avoid polluting global scope.
```javascript
(function(){
    // declaration
})();

(() => {
    // declaration
});
```

## Local Storage and Session Storage
These are two web storage options available in mordern browsers, allows us to stored "key-value" pairs locally on user's device without sending it to server.
<br>
| Attributes |Local Storeage | Session Storage |
| -------------- | -------------- | --------------- |
| Lifetime and Persistance | persists across browser sessions | data is tied to session |
| Scope | accessible across tabs/windows | accessible to only same tab and window |
| Expiration | data remains stored until explicitly | data is cleared when session ends |
| Usecases | when we want data to persist across session and accessible across multiple tabs | when we want data to be available only for duration of single session and within same tab/window |


## Cookies and Sessions

| Attributes | Cookie | Sessions |
| -------------- | -------------- | --------------- |
| Use | used for client-side tracking, storing user preferences, and maintaining state across requests.| used for server-side storage of more sensitive data of maniting user-specific information. |
| Storage location | client side. | server side. |
| Data persistance | cookies have an expiration time and can persist beyond single session if specified. | sessions ends when user closes browser of after a certain period of inactivity. |
| Security | less secure. | more secure. |

## JS Runtime
![Js Runtime Image](https://excalidraw.com/#json=uKsIafaM2qDSKvckeTl15,yKiZyonfFuhtBqxCp0hOXA)