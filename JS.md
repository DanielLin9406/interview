# Javascript

## Index of Topic

- Data type
- Prototype
- Scope/Context/Closure
- OO
  - this/call/apply/bind
  - new
  - Inheritance
  - Object
- Async Programing
- GC
- V8

## Data type

### What is the difference between Double Equals vs Triple Equals?

> - Double equals also performs type coercion.
> - Type coercion means that two values are compared only after attempting to convert them into a common type.

### Test if it is an array

- Object.prototype.toString.call()
- instanceof
- Array.isArray()

> - Object.prototype.toString.call() work for all primitive types

> instanceof: whether there is a prototype of a type
> `[] instanceof Array; // true`
> but only work on object type, primitive type is not working`[] instanceof Object; // true`

> Array.isArray is better than instanceof for testing iframe

```
var iframe = document.createElement('iframe');
document.body.appendChild(iframe);
xArray = window.frames[window.frames.length-1].Array;
var arr = new xArray(1,2,3); // [1,2,3]

// Correctly checking for Array
Array.isArray(arr);  // true
Object.prototype.toString.call(arr); // true
// Considered harmful, because doesn't work though iframes
arr instanceof Array; // false
```

> Array.isArray() is ES5 method; Use Object.prototype.toString.call() if the requirement is not meet.

```
if (!Array.isArray) {
  Array.isArray = function(arg) {
    return Object.prototype.toString.call(arg) === '[object Array]';
  };
}
```

Ref.[第 21 题：有以下 3 个判断数组的方法，请分别介绍它们之间的区别和优劣 Object.prototype.toString.call() 、 instanceof 以及 Array.isArray()](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/23)

## Prototype

## Closure

## Context

## Scope

## this/call/apply/bind

### this

"this" is defined by the way that how to call it.

## Async Programing

## Object

## GC

## V8
