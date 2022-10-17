# Review: Objects & the value of `this`

[TOC]

Contents from *[Here](https://cs.nyu.edu/courses/fall22/CSCI-UA.0467-001/_site/slides/js/objects-prototypes.html?print-pdf#/1)* and *[Here](https://cs.nyu.edu/courses/fall22/CSCI-UA.0467-001/_site/slides/05/not-arrow.html?print-pdf#/)*

## Object-Oriented Programming

**Describe the following object oriented programming concepts**: →

- **inheritance** - basing a class off of another class so that it maintains the same behavior as its super class
- **polymorphism** - having the same interface to instances of different types
- **encapsulation** - information hiding, internals/implementation details not accessible publicly
- **abstraction** - (again) creating tools / interfaces that allow a programmer to address the actual problem they're solving rather than having to deal with necessary, but irrelevant (to the problem) details

### Java 

* **inheritance** - subclassing… using extend
* **polymorphism** - instances of different classes that are subclasses of the same superclass
* **encapsulation** - private methods and private members variables
* **abstraction** - creating classes, interfaces, abstract classes, and methods

### JavaScript

* inheritance - prototypes and/or functions
* polymorphism - *duck typing*
* encapsulation - closures
* abstraction - higher order functions, prototypes, etc.



## The value of `this`

### Strict Mode vs Sloppy Mode

* The value of `this` is different in <u>Strict Mode</u> and <u>Sloppy Mode</u>

    * In ESM or Strict Mode, when called as a regular function: `this` will be `undefined` (you will likely get an error because `this.propName`, cannot read prop off of undefined
    * In CJs or "Sloppy" Mode,`this` will be the global object 

    ```javascript
    const f = function() {
    	console.log('this is', this);
    }
    f();
    // In strict mode: this is undefined
    // In sloppy mode: this is <Window or Global Object>
    ```

* using `call` `apply` or `bind`

    * `this` is whatever you set it to be!

    ```javascript
    function greet(firstName, lastName) { 
        console.log(this.greeting, firstName, lastName); 
    }
    const obj = { greeting: 'hi' };
    
    greet("JOE", "VERSOZA");   //undefined 'JOE' 'VERSOZA'
    
    greet.call(obj, 'joe', 'versoza');    //hi joe versoza
    
    greet.apply(obj, ['Joe', 'Versoza']);    //hi Joe Versoza
    
    const greetToad = greet.bind(obj, "toad");
    greetToad("worshiper");  //hi toad worshiper
    ```


### `this` in Arrow Functions

* Using regular anonymous function definition:

    ```javascript
    const counter = {numbers: [1, 2, 3, 4], animal:'owl'};
    counter.count = function() {
        this.numbers.forEach(function(n) {
            console.log(n, this.animal + (n > 1 ? 's' : ''));
        });
    };
    counter.count();
    
    // error - `this` is `undefined`
    ```

    * This is because the anonymous function is being invoked as a **regular function** for every element in the `Array`, `counter.numbers`. 
    * **`this` refers to `undefined`**, which causes an error on property lookup
    * Same thing happens in Sloppy mode where `this` is global object and `this.animal` is still `undefined`

* Using <u>Arrow Functions</u> to fix it

    ```javascript
    const counter = {numbers: [1, 2, 3, 4], animal:'owl'};
    counter.count = function() {
        this.numbers.forEach((n) => {
            console.log(n, this.animal + (n > 1 ? 's' : ''));
        });
    };
    counter.count();
    
    // 1 'owl'
    // 2 'owls'
    // 3 'owls'
    // 4 'owls'
    ```

    * The `this` value in **arrow functions** is the `this` in the scope that the arrow function was created in 
    * Here, `this` is whatever `this` refers to in the count method, and because `count` was invoked as a method, `this` is the object that `count` was called on.

### Summary

<u>What is this?</u>

1. regular function invocation
    - in ES Modules / strict mode, `this` is `undefined`
    - in sloppy mode, `this` is the global object
2. method call
    - `this` is the object the method was called on
3. invoked with call or apply
    - `this` is the first argument passed in to call or apply
4. arrow function
    - `this` is `this` from the enclosing context

## When not to use Arrow Functions

Arrow functions are useful and can fix the value of `this`, but there are some places where **they don't work quite right**.

- creating constructors
- creating methods
    - either on object literals
    - or on prototypes
- (not relevant now, but) creating `addEventListener` callbacks where you want `this` to refer to the element that generated the event

### Can't be Constructors

**In the following code, we try to use an arrow function as a constructor.** →

```javascript
const Cat = (name) => {
    this.name = name;
}
var c = new Cat();
        ^
TypeError: Cat is not a constructor
```

Instead, use the usual function declaration to create constructors:

```javascript
function Cat(name) {
    this.name = name;
}
```

### Arrow Functions as Methods

```javascript
function Cat(name) {
    this.name = name;
}
Cat.prototype.meow = (() => {
    console.log(this.name, 'meows');
});
var c = new Cat('paw newman');

c.meow();
//undefined meows
```

* This happens because arrow functions do not bind a new value to `this`

- again, `this` remains the same as the `this` in the containing context / scope
    - In this case it's the global object

### Arrow Functions as Methods on Object Literals

```javascript
const cat = {
    sound: 'meow',
    meow: () => {console.log(this.sound);}
};
cat.meow();

//undefined
```

Make some change to it

```javascript
const cat = {
    sound: 'meow'
};
cat.meow = function(){
    const f = () => {
        console.log(this.sound);
    }
    f.call()
}
cat.meow();
//meow
```

### Arrow Functions and `addEventListener`

**To be complete… be careful when using arrow functions and `addEventListener`** →

Starting with this code:

```javascript
const button = document.createElement('button');
document.body.appendChild(button).textContent = 'Click Me';
```

The following listeners alert different messages!

```javascript
// alerts window object (essentially global)
button.addEventListener('click', () => {alert(this)});
// alerts button element
button.addEventListener('click', function()  {alert(this)});
```

- if you want `this` in your event handler to reference the element event's target element, then use function expressions
- …because arrow functions don't create their own `this`, and instead use the `this` from the surrounding context