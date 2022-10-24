# Review: Objects & Prototypes

[TOC]

From https://cs.nyu.edu/courses/fall22/CSCI-UA.0467-001/_site/slides/05/prototypes.html?print-pdf#/

## Prototype

**All objects have a link to another object that's called its `[[prototype]]`**.

- note that `[[prototype]]` means the concept, *prototype* not the actual syntax (confusingly, there are properties and objects in JavaScript that are named `prototype` but are not exactly the concept `[[prototype]]`)
- **objects** are basically just a **collection of properties**
- when an objects gets a request for a **property that it doesn't have, the object's prototype is searched for that property**
- prototype objects have prototypes as well!
- searching goes on up the chain of prototypes until
    - the property is found
    - an object with a `null` prototype is reached / the last object in the chain: `Object.prototype`

### Object.prototype

The top level prototype is [Object.prototype](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/prototype):

- all objects in JavaScript are descended from `Object`
- all objects inherit methods and properties from `Object.prototype`
- **`Object.prototype`'s [[prototype]] is `null`**

```javascript
console.log(
	Object.getPrototypeOf({}) == Object.prototype);// true

console.log(
	Object.getPrototypeOf(Object.prototype)); // null
```

`Object.prototype` provides a bunch of <u>methods</u> and <u>properties</u> to all JavaScript objects

- `toString()`
- `hasOwnProperty()`

`Object.prototype` isn't always an object's direct [[prototype]]; instead, most objects have a [[prototype]] of another object

- **functions** derive from `Function.prototype`
- **arrays** derive from `Array.prototype`

### Using `Object.create`

**`Object.create`** - creates a new object with the specified [[prototype]] object and properties

```javascript
// our "template" object
const protoWerewolf = { 
	description: 'hairy', 
	howl: function(thing) {
		console.log('The werewolf howls at the ' + thing + '.');
	}
};

// make a new werewolf with Object.create
const sadWerewolf = Object.create(protoWerewolf);
sadWerewolf.mood = 'sullen';
sadWerewolf.howl('moon');
```

> It turns out, for inheritance, it's common to use `Object.create(MyObj.prototype)` … we'll see why later

## Constructors

Another way to create an object with a particular prototype is to use a **constructor**.

- a **constructor** is basically just a function with the `new` keyword in front of it

    > it's a convention to make the first letter of a constructor uppercase
    >
    > this helps distinguish between regular functions and constructors

- an **instance** is an object created by using **`new`**

- a constructor's **`this`** object is bound to a **fresh, empty object**

    - this is the object that's returned from invoking the constructor with `new` (unless the constructor explicitly returns a different object)

### Constructor.Prototype

**All constructors have a property named `prototype`.**

- the default value of a constructor's prototype is a plain, empty object that derives from `Object.prototype`
- every instance created with the constructor will have `constructor.prototype` as its *actual* prototype
    - note that there's a difference between the **`constructor.prototype`** versus the **constructor's *actual* prototype** →**`Function.prototype`**
- We could use a constructor's prototype to add a howl method on every instance of Werewolf

```javascript
Werewolf.prototype.howl = function(thing) {
	console.log('The werewolf howls at the ' + thing + '.');
}
sadWerewolf.howl('moon');
partyWerewolf.howl('bowl of chips');
```

* When we added a property to the constructor's prototype, **the instances immediately had access to the new property**, even though they were instantiated before the prototype was set.

    >  it's typical for a prototype object to **only** contain methods

```javascript
function Werewolf(mood) {
	this.mood = mood;
}
const partyWerewolf = new Werewolf('partying'); 

Werewolf.prototype.clothing = 'tattered shirt';
console.log(partyWerewolf.clothing);
// tattered shirt
console.log(Object.hasOwn(partyWerewolf,"clothing"))
// false
```

## "Inherited" Properties

### `in` operator

The **`in` operator** returns `true` if the specified property is in the specified object or its prototype chain.

```javascript
const numbers = [1, 2, 3, 4];
console.log('toString' in numbers);

true
```



### Overriding Properties

* If you add a property directly to an object, it is added to the object *itself*, not the object's prototype. 

```javascript
function Werewolf(mood) {
	this.mood = mood;
}
const partyWerewolf = new Werewolf('partying'); 

Werewolf.prototype.clothing = 'tattered shirt';
console.log(partyWerewolf.clothing);
// tattered shirt
console.log(Object.hasOwn(partyWerewolf,"clothing"))
// false

partyWerewolf.clothing = "backwards cap"
console.log(Object.hasOwn(partyWerewolf,"clothing"))
// true
```

**when you add a property to an object, that property is added to the object itself…**

* if there is a property with the same name in the prototype, it is *masked* or **overridden** by the new property
* note that the prototype itself is not changed

### Where do Properties come from?

<u>**Use `partyWerewolf` as an example**</u>

* from `partyWerewolf` object
    * `clothing`: "backwards cap"
    * `mood`: "partying"
* from `Werewolf.prototype`
    * `clothing`: "tattered shirt" <u>(masked)</u>
    * `howl`: (function)
* from `Object.prototype`
    * `toString`: (function)
    * etc.

## Inheritence

### Pattern of Inheritence

Using our parent constructor, `Werewolf`

```javascript
function Werewolf(mood) {
    this.mood = mood;
}
Werewolf.prototype.howl = function(thing) {
	console.log('The werewolf howls at the ' + thing + '.');
}
```

Create a constructor for a space werewolf (!!!) by setting its prototype to a new object who's prototype is `Werewolf.prototype`

```javascript
function SpaceWerewolf() {}
SpaceWerewolf.prototype = Object.create(Werewolf.prototype);
```

However, the prototype only contains methods

```javascript
const w = new SpaceWerewolf();
console.log(mood)

ReferenceError: mood is not defined
```

we can execute the parent constructor using `call`

```javascript
function SpaceWerewolf(mood) {
    Werewolf.call(this, mood);
}
```

### Constructor Property

All object's have a property named `constructor`. **`constructor`** is the function that was used to create the instance's prototype.

```javascript
const a = [];
console.log(a.constructor); // [Function: Array] 
```

So we should probably set that on our child constructor's prototype property explicitly so that all objects created from `SpaceWerewolf` have that as its constructor.

```javascript
SpaceWerewolf.prototype.constructor = SpaceWerewolf;
```

### Example

```javascript
function Monster() {
	this.scary = true;
}
Monster.prototype.boo = function() { console.log('Boo!');}

function Werewolf(mood) {
    Monster.call(this);
	this.mood = mood;	
}
Werewolf.prototype = Object.create(Monster.prototype);
Werewolf.prototype.constructor = Werewolf;
Werewolf.prototype.howl = function(thing) {
	console.log('The werewolf howls at the ' + thing + '.');
}
const sadWerewolf = new Werewolf('sad');
const partyWerewolf = new Werewolf('partying');
partyWerewolf.scary = false;

console.log(sadWerewolf.scary);    // true
console.log(partyWerewolf.scary);  // false
partyWerewolf.boo();               // Boo!
```

Some notes on the example:

- to inherit properties from Monster…
    - we set our Werewolf constructor's prototype to a fresh object with `Monster.prototype` as the prototype
    - we called the "super" constructor
- `const sadWerewolf = new Werewolf('sad');`
- …which is why scary was found in the prototype chain for `sadWerewolf`

## Properties of the class

### Enumertaion properties

```javascript
for (const prop in obj) {
	console.log(prop)
}
```

```javascript
for (const p in partyWerewolf) {
	console.log(p + ': ' + partyWerewolf[p]);
}
for (const p in sadWerewolf) {
	console.log(p + ': ' + sadWerewolf[p]);
}
```

### Own Property

* Check for the properties that were **explicitly set on our object**, rather than including inherited ones.
    * `hasOwnProperty`
    * `Object.hasOwn`

## `instanceof`

If you have an object, and you'd like to know what constructor it came from, you can use the **`instanceof`** operator.

- instance on left
- constructor on right

```javascript
console.log(myCar instanceof Car); // true
console.log(myCar instanceof Bike);// false
```

> In *actuality* instance of checks **if an object has in its prototype chain the prototype property of a constructor**

