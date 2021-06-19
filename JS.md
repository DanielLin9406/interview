# Javascript

## Index of Topic

- Loops
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

## Loops

> - Speed:  
>   for > ... > for-in

Ref. [JavaScript 遍歷 Array 的四種方法：for、for-in、for-of、forEach()](https://tigercosmos.xyz/post/2021/06/js/js-array-for-methods/?fbclid=IwAR2Bj9L6e2T4SkcqXn3i7dh4CYbXEWluvhMHzpzWdXOVWLYtaaDtL_q0Bwc)

### for

- fastest method

```js
for (let i = 0; i < 5; i++) {
  //code block 執行指令（區塊）
  console.log(i);
}

const list = ["asdfa", "dfdf", "ssss"];
for (let i = 0; i < list.length; i++) {
  let html = `<div>${list[i]}</div>`;
  console.log(html);
}
```

```js
var list = ["My", "name", "is", "Ben"];

for (var i = 0; i < list.length; i++) {
  console.log(list[i]); // result: "My","name"
  if (list[i] === "name") {
    break;
  }
}

var list = ["My", "name", "is", "Ben"];

function breakForLoop(arrayToBreak) {
  for (var i = 0; i < arrayToBreak.length; i++) {
    console.log(arrayToBreak[i]); //result: "My","name"
    if (arrayToBreak[i] === "name") {
      return false;
    }
  }
}

breakForLoop(list);
```

Ref. [JavaScript 遍歷 Array 的四種方法：for、for-in、for-of、forEach()](https://tigercosmos.xyz/post/2021/06/js/js-array-for-methods/?fbclid=IwAR2Bj9L6e2T4SkcqXn3i7dh4CYbXEWluvhMHzpzWdXOVWLYtaaDtL_q0Bwc)

Ref.[How to break when looping an array in Javascript](https://medium.com/@benjamincherion/how-to-break-an-array-in-javascript-6d3a55bd06f6)

### for-in

> - ES1
> - Through all the keys in Object
> - All the properties include itself and inherit

```js
const arr = ["a", "b", "c"];
arr.prop = "property value";

for (const key in someArray) {
  console.log(key);
}

// Output:
// '0'
// '1'
// '2'
// 'prop'
```

> Ref. [JavaScript 遍歷 Array 的四種方法：for、for-in、for-of、forEach()](https://tigercosmos.xyz/post/2021/06/js/js-array-for-methods/?fbclid=IwAR2Bj9L6e2T4SkcqXn3i7dh4CYbXEWluvhMHzpzWdXOVWLYtaaDtL_q0Bwc)

### for-of

- Basic form

```js
for (const elem of someArray) {
  console.log(elem);
}
```

- Break loop

```js
var list = ["My", "name", "is", "Ben"];

for (let elem of list) {
  console.log(elem); //result: "My","name"
  if (elem === "name") {
    break;
  }
}

var list = ["My", "name", "is", "Ben"];

function breakForOfLoop(arrayToBreak) {
  for (let elem of arrayToBreak) {
    console.log(elem); //result: "My","name"
    if (elem === "name") {
      return false;
    }
  }
}

breakForOfLoop(list);
```

- If you need index

```js
const arr = ["chocolate", "vanilla", "strawberry"];

for (const index of arr.keys()) {
  console.log(index);
}
// Output:
// 0
// 1
// 2
```

- If you need both key and value

```js
const arr = ["chocolate", "vanilla", "strawberry"];

for (const [index, value] of arr.entries()) {
  console.log(index, value);
}
// Output:
// 0, 'chocolate'
// 1, 'vanilla'
// 2, 'strawberry'
```

- Loop through Map

```js
const myMap = new Map().set(false, "no").set(true, "yes");

for (const [key, value] of myMap) {
  console.log(key, value);
}

// Output:
// false, 'no'
// true, 'yes'
```

Ref. [JavaScript 遍歷 Array 的四種方法：for、for-in、for-of、forEach()](https://tigercosmos.xyz/post/2021/06/js/js-array-for-methods/?fbclid=IwAR2Bj9L6e2T4SkcqXn3i7dh4CYbXEWluvhMHzpzWdXOVWLYtaaDtL_q0Bwc)

Ref.[How to break when looping an array in Javascript](https://medium.com/@benjamincherion/how-to-break-an-array-in-javascript-6d3a55bd06f6)

### while

### do/while

### Array.prototype.forEach()

> - No effect on original array
> - Can not use await nor break
> - Keep variable inside the callback block

```js
const arr = ["a", "b", "c"];
arr.prop = "property value";

arr.forEach((elem, index) => {
  console.log(elem, index);
});

// Output:
// 'a', 0
// 'b', 1
// 'c', 2
```

> - check some() or every() if you need break in loop

Ref. [JavaScript 迴圈控制方法之 — -for/for…in/forEach](https://medium.com/web-design-zone/%E8%BF%B4%E5%9C%88%E6%8E%A7%E5%88%B6%E6%96%B9%E6%B3%95%E4%B9%8B-for-for-in-foreach-4ee9fe83ef7a)
Ref. [JavaScript 遍歷 Array 的四種方法：for、for-in、for-of、forEach()](https://tigercosmos.xyz/post/2021/06/js/js-array-for-methods/?fbclid=IwAR2Bj9L6e2T4SkcqXn3i7dh4CYbXEWluvhMHzpzWdXOVWLYtaaDtL_q0Bwc)

### Array.prototype.every()

> - The every() method will test all elements of an array (all elements must pass the test).

```js
var list = ["My", "name", "is", "Ben"];

list.every(function (elem) {
  console.log(elem); //result: "My","name"
  if (elem === "name") {
    return false;
  }
  return true;
});
```

Ref.[How to break when looping an array in Javascript](https://medium.com/@benjamincherion/how-to-break-an-array-in-javascript-6d3a55bd06f6)

### Array.prototype.some()

> - The some() method will test all elements of an array (only one element must pass the test)

```js
var list = ["My", "name", "is", "Ben"];

list.some(function (elem) {
  console.log(elem); //result: "My","name"
  if (elem === "name") {
    return true;
  }
  return false;
});
```

Ref.[How to break when looping an array in Javascript](https://medium.com/@benjamincherion/how-to-break-an-array-in-javascript-6d3a55bd06f6)

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

```js
var iframe = document.createElement("iframe");
document.body.appendChild(iframe);
xArray = window.frames[window.frames.length - 1].Array;
var arr = new xArray(1, 2, 3); // [1,2,3]

// Correctly checking for Array
Array.isArray(arr); // true
Object.prototype.toString.call(arr); // true
// Considered harmful, because doesn't work though iframes
arr instanceof Array; // false
```

> Array.isArray() is ES5 method; Use Object.prototype.toString.call() if the requirement is not meet.

```js
if (!Array.isArray) {
  Array.isArray = function (arg) {
    return Object.prototype.toString.call(arg) === "[object Array]";
  };
}
```

Ref.[第 21 题：有以下 3 个判断数组的方法，请分别介绍它们之间的区别和优劣 Object.prototype.toString.call() 、 instanceof 以及 Array.isArray()](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/23)

## Prototype

## Closure

## Context

## OO

### Scope

### this/call/apply/bind

### this

"this" is defined by the way that how to call it.

### Inheritance

```js
function Child(value) {
  Parent.call(this);
  this.prop = value;
}

Child.prototype = Object.create(Parent.prototype);
Child.prototype.constructor = Child;
Child.prototype.method = "...";

//or
// Child will own all methods of the Parent has
Child.prototype = new Parent();
```

```js
// Parent
function Shape() {
  this.x = 0;
  this.y = 0;
}
Shape.prototype.move = function (x, y) {
  this.x += x;
  this.y += y;
  console.info("Shape moved.");
};

// Step1 version1
function Rectangle() {
  Shape.call(this);
}
// Step1 version2
function Rectangle() {
  this.base = Shape;
  this.base();
}

// Step2，子类继承父类的原型
Rectangle.prototype = Object.create(Shape.prototype);
Rectangle.prototype.constructor = Rectangle;

var rect = new Rectangle();

rect instanceof Rectangle; // true
rect instanceof Shape; // true
```

- Miltiple Inheritance

```js
function M1() {
  this.hello = "hello";
}

function M2() {
  this.world = "world";
}

function S() {
  M1.call(this);
  M2.call(this);
}

// Inheritance M1
S.prototype = Object.create(M1.prototype);
// Inheritance M2 by add M2's prototype on the chain
Object.assign(S.prototype, M2.prototype);
S.prototype.constructor = S;

var s = new S();
s.hello; // 'hello'
s.world; // 'world'
```

Ref.[对象的继承](https://wangdoc.com/javascript/oop/prototype.html)

## Async Programing

## Object

## GC

## V8
