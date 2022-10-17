# Review: ES6 Classes

[TOC]

From https://cs.nyu.edu/courses/fall22/CSCI-UA.0467-001/_site/slides/05/prototypes.html?print-pdf#/

## ES6 Classes

In ES6, there's yet another way to create a prototype chain of objects, and that's using a *familiar* construct, **classes**.

- they're syntactic sugar for creating constructor functions and a prototype object with methods
- (in actuality, everything is still prototypes and constructor functions)

## Example ES6 Class

**These two bits of code both produce a function called `HttpRequest`!** →

ES6 class:

```
class HttpRequest {
}
```

ES5 constructor:

```
function HttpRequest() {
}
```

Both result in the same output when used in the following manner:

```
const req = new HttpRequest();
console.log(HttpRequest);
console.log(typeof req.constructor);
console.log(req.constructor.name);
```

## Constructors

ES6 style classes allow for a constructor to be defined as follows:

- within the class definition, create a function called constructor
- no function keyword is required
- the constructor has access to `this` which represents the instance that is created



```
class HttpRequest {
    constructor(method, url) {
        this.method = method;
        this.url = url;
    }
}
```

The above code is *mostly* the same as this ES5 function that can be used as a constructor:

```
function HttpRequest(method, url) {
   this.method = method;
   this.url = url;
}
```

We'll see later that subclass constructors must call super before using `this`.

## Methods in ES5

**In ES5, to add a method to the prototype, we'd have to do something like this:**→

```
function HttpRequest(method, url) {
   this.method = method;
   this.url = url;
}
HttpRequest.prototype.makeRequest = function() {
    return this.method + ' ' + this.url + ' HTTP/1.1';
}
```

## Methods in ES6

**In ES6, we can define methods directly in the class definition, and they will show up in the instances' prototype** →

```
class HttpRequest {
  constructor(method, url) {
    this.method = method;
    this.url = url;
  }

  makeRequest() {
    return this.method + ' ' + this.url + ' HTTP/1.1';
  }
}
```

- note that there are no commas between method and constructor definitions
- again, you do not have to use the keyword, `function`
- methods, of course, can reference `this`, and if the method is called within the context of an instance, then `this` refers to the instance

## ES6 Methods Continued

**Note that creating these methods in ES6 style classes is \*actually\* just adding to the prototype!** →

```
const req = new HttpRequest('GET', 'http://foo.bar/baz');
console.log(req.makeRequest());
console.log(Object.getPrototypeOf(req).makeRequest);
```

## Inheritance

**Use `extends` to inherit from a class!** (read: set up a prototype chain)

```
class Element {
    constructor(name) {
        this.name = name; 
    }
}
class ImgElement extends Element {
    // make sure to call super before using this
    // within subclass
    constructor(url) {
        super('img');
        this.url = url;
    }
}
const img = new ImgElement('http://foo.bar/baz.gif');
console.log(img.name);
console.log(img.url);
```

## Calling Super Constructor

**In the previous example, `super` was used to call the base class constructor.** →

- `super` must be called in your subclass constructor if…
- you use `this` within your constructor
- (it's essentially initializing `this` properties the way that the superclass would
- **`super` must be called before using this within a subclass**

## High Level Summary

**Every object in JavaScript links to another object called its [[prototype]].** →

- when a property cannot be found in the original object, it goes up the prototype chain
- objects can be given prototypes in 3 ways:
    1. `Object.create`
    2. constructor functions
    3. ES6 Classes
    4. (there's also something called `__proto__` that allows direct access to a [[prototype]], but its use is discouraged)