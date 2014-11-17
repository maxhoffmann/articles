---
date: 2014-03-10
---
# Object-Based JavaScript in ES6

At first I was pretty happy, that there will be a `class` syntax in ECMAScript 6. Then I listened to the [latest revision](http://workingdraft.de/160/) of “Working Draft” (German podcast) about Node and JavaScript and afterwards watched Eric Elliott’s talk [“Classical Inheritance is obsolet”](https://vimeo.com/69255635) for a second time. It became clear to me that class-based object-oriented programming may not be my programming paradigm of choice. Instead I prefer a truly “object-oriented” programming style or as Kyle Simpsons calls it: [“object-based”](http://davidwalsh.name/javascript-objects-deconstruction).

Although the `class` syntax of ES6 will allow writing JavaScript in a class-based way more easily, there is also some syntactical sugar for the “object-based” approach.

## Enhanced Object Literals

Besides a shorthand for `property: property` assignments, methods can now be defined without the `function` keyword.

```javascript
var human = {
  breathe() { // no function keyword here
    return 'breathing…';
  }
};
```

## Object.setPrototypeOf

The most important addition for me is `Object.setPrototypeOf`. It allows defining objects using the enhanced object literal and linking these objects afterwards via the prototype chain to embrace its “behavior delegation”.

Before ES6 one had to use `Object.create`, which prevents using the object literal on the object delegating its behavior.

```javascript
var human = {
  breathe() {
    return 'breathing…';
  }
};

var worker = Object.create(human);

worker.work = function() {
  return 'working…';
};
worker.company = 'best company in the world';

worker.breathe();
// returns 'breathing…';
```

With `Object.setPrototypeOf` the usage of two object literals will be possible.

```javascript
var human = {
  breathe() {
    return 'breathing…';
  }
};

var worker = {
  work() {
    return 'working…';
  },
  company: 'best company in the world'
};

Object.setPrototypeOf(worker, human);

worker.breathe();
// returns 'breathing…';
```

This allows using the object-based approach as it was intended.

## Object.assign

Instance-specific behavior or behavior that should be available to multiple prototypes can be achieved with mixins.

> A mixin is a class that defines a set of functions relating to a type. — [Angus Croll](http://javascriptweblog.wordpress.com/2011/05/31/a-fresh-look-at-javascript-mixins/)

Instead of using classes one can simply create an object with the desired functionality and copy its behavior to another object or prototype via `Object.assign`.

```javascript
var canEat = {
  food: 'nothing',
  eat() {
    return `eats ${this.food}`; // template string (part of ES6)
  }
};

Object.assign(worker, canEat);

worker1 = Object.create(worker);
worker2 = Object.create(worker);
worker2.food = 'apple';

worker1.eat(); // 'eats nothing'
worker2.eat(); // 'eats apple'
```

## Conclusion

Although ES6 offers the `class` syntax it also provides syntactic sugar for prototypes and their concept of “behavior delegation”. I look forward to using ES6 in production.
