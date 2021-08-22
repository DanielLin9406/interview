# Coding

## Index of Contents

- Object
  - [Object.create](#objectcreate)
  - [instanceof](#instanceof)
  - [new](#new)
- Copy
  - Shallow Copy
  - Deep Copy
- Promise
  - Promise
  - Promise.then
  - Promise.all
  - Promise.race
- Array
  - Intersect
  - Merge
- this
  - call
  - apply
  - bind
- Function
  - currying
- Async
- Class
- Ajax
  - Promise 封裝

## Object

### Object.create

- 以 obj 作為 template 生成新的 function

```js
function create(obj) {
  function F() {}
  F.prototype = obj;
  return new F();
}
```

> Ref. [手写 Object.create](https://juejin.cn/post/6946136940164939813#heading-2)

### Instanceof

- Test whether the prototype of a constructor exist in the prototype chain of a object.

```js
function myInstanceOf(instance, constructor) {
  let constructorPrototype = constructor.prototype;
  // let proto = instance.__proto__
  let proto = Object.getPrototypeOf(instance);

  while (true) {
    if (!proto) return false;
    if (proto === constructorPrototype) return true;

    proto = Object.getPrototypeOf(proto);
  }
}
```

> Ref. [手写 Object.create](https://juejin.cn/post/6946136940164939813#heading-2)

- 左邊的一直往.`__proto__` 往上找，看有沒有右邊

```js
function Foo() {}

Object instanceof Object; // true
Function instanceof Function; // true
Function instanceof Object; // true
Foo instanceof Foo; // false
Foo instanceof Object; // true
Foo instanceof Function; // true
```

```js
leftValue = Object.__proto__ = Function.prototype;
rightValue = Object.prototype;
// 第一次判断
leftValue != rightValue;
leftValue = Function.prototype.__proto__ = Object.prototype;
// 第二次判断
leftValue === rightValue;
// 返回 true
```

```js
(leftValue = Foo), (rightValue = Foo);
leftValue = Foo.__proto = Function.prototype;
rightValue = Foo.prototype;
// 第一次判断
leftValue != rightValue;
leftValue = Function.prototype.__proto__ = Object.prototype;
// 第二次判断
leftValue != rightValue;
leftValue = Object.prototype = null;
// 第三次判断
leftValue === null;
// 返回 false
```

> Ref.[浅谈 instanceof 和 typeof 的实现原理](https://juejin.cn/post/6844903613584654344)

### New

- create a empty object and set new object's `__proto__` to fn.prototype
- bind `this` of the fn to obj
- return ret if

```js
function _new(fn, ...arg) {
  const obj = Object.create(fn.prototype);
  const ret = fn.apply(obj, arg);
  return ret instanceof Object ? ret : obj;
}
```

Ref. [第 14 题：如何实现一个 new ](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/12)

## Copy

Before copying, need to loop through all the keys of object

### Shallow Copy

#### Object.assign

> Object.assign(target, source_1, ···)
> Note
>
> - If target and source share the same properties, the later one overlap the former one.
> - If parameter is object, return object; otherwise, the parameter will be turned into an object and return that.
> - null and undefined cannot be turn into an object, so they can not be the first parameter

```js
let target = { a: 1 };
let object2 = { b: 2 };
let object3 = { c: 3 };
Object.assign(target, object2, object3);
console.log(target); // {a: 1, b: 2, c: 3}
```

Ref.[高频前端面试题汇总之手写代码篇](https://juejin.cn/post/6946136940164939813#heading-24)

#### Spread Operator

```js
let obj1 = { a: 1, b: { c: 1 } };
let obj2 = { ...obj1 };
obj1.a = 2;
console.log(obj1); //{a:2,b:{c:1}}
console.log(obj2); //{a:1,b:{c:1}}

obj1.b.c = 2;
console.log(obj1); //{a:2,b:{c:2}}
console.log(obj2); //{a:1,b:{c:2}}
```

Ref.[高频前端面试题汇总之手写代码篇](https://juejin.cn/post/6946136940164939813#heading-24)

#### Array.slice and Array.concat

- slice(): won't modify the original one

```js
let arr = [1, 2, 3, 4];
arr.slice() === arr; // false
```

- concat(): won't modify the original one

```js
let arr = [1, 2, 3, 4];
arr.concat() === arr; // false
```

Ref.[高频前端面试题汇总之手写代码篇](https://juejin.cn/post/6946136940164939813#heading-24)

#### Shallow Copy From Scratch

- ES5: for-in + hasOwnProperty => get own enumerable properties

```js
function shallowCopy(object) {
  // 只拷贝对象
  if (!object || typeof object !== "object") return;

  // 根据 object 的类型判断是新建一个数组还是对象
  let newObject = Array.isArray(object) ? [] : {};

  // 遍历 object，并且判断是 object 的属性才拷贝
  for (let key in object) {
    if (object.hasOwnProperty(key)) {
      newObject[key] = object[key];
    }
  }

  return newObject;
}
```

Ref.[高频前端面试题汇总之手写代码篇](https://juejin.cn/post/6946136940164939813#heading-24)

- ES5: getOwnPropertyNames + getOwnPropertyDescriptor => get own enumerable or innumerable properties

```js
function copyObject(orig) {
  var copy = Object.create(Object.getPrototypeOf(orig));
  copyOwnPropertiesFrom(copy, orig);
  return copy;
}

function copyOwnPropertiesFrom(target, source) {
  Object.getOwnPropertyNames(source).forEach(function (propKey) {
    var desc = Object.getOwnPropertyDescriptor(source, propKey);
    Object.defineProperty(target, propKey, desc);
  });
  return target;
}
```

Ref.[Object 对象的相关方法](https://wangdoc.com/javascript/oop/object.html#objectprototypeisprototypeof)

- ES6: getOwnPropertyDescriptors

```js
function copyObject(orig) {
  return Object.create(
    Object.getPrototypeOf(orig),
    Object.getOwnPropertyDescriptors(orig)
  );
}
```

### Deep Copy

#### JSON.stringify()

> - Note: function, undefined, symbol are all gone after JSON.stringify()

```js
let obj1 = {
  a: 0,
  b: {
    c: 0,
  },
};

let obj2 = JSON.parse(JSON.stringify(obj1));
```

#### lodash cloneDeep

#### Deep Copy From Scratch

```js
function deepCopy(object) {
  if (!object || typeof object !== "object") return;
  let newObject = Array.isArray(object) ? [] : {};
  for (let key in object) {
    if (object.hasOwnProperty(key)) {
      newObject[key] =
        typeof object[key] === "object"
          ? deepCopy(object[key])
          : newObject[key];
    }
  }
  return newObject;
}
```

Ref.[高频前端面试题汇总之手写代码篇](https://juejin.cn/post/6946136940164939813#heading-26)

---

## Promise

### Promise

### Promise.then

### Promise.all

### Promise.race

---

## Array

### Array Intersect

```js
const intersect = (arr1, arr2) => {
  const map {}
  const res = []
  for (let n of arr1){
    if (map[n]){
      map[n]++
    } else {
      map[n] = 1
    }
  }
  for (let n of arr2){
    if (map[n]>0){
      res.push(n)
      map[n]--
    }
  }
  return res
}
```

Ref.: [第 59 题：给定两个数组，写一个方法来计算它们的交集。](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/102)

### Array Merge

> > >

- ES5

```js
var array1 = ["Vijendra", "Singh"];
var array2 = ["Singh", "Shakya"];

console.log(array1.concat(array2));
```

- ES6

```js
const array1 = ["Vijendra", "Singh"];
const array2 = ["Singh", "Shakya"];
const array3 = [...array1, ...array2];
```

```js
var c = [...a, ...b.filter((o) => a.indexOf(o) !== -1)];
```

```js
var c = [...new Set([...a, ...b])];
```

Ref.[How to merge two arrays in JavaScript and de-duplicate items](https://stackoverflow.com/questions/1584370/how-to-merge-two-arrays-in-javascript-and-de-duplicate-items)

Ref.[第 30 题：请把俩个数组 [A1, A2, B1, B2, C1, C2, D1, D2] 和 [A, B, C, D]，合并为 [A1, A2, A, B1, B2, B, C1, C2, C, D1, D2, D]](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/39)

> > >

### 随机生成一个长度为 10 的整数类型的数组，例如 [2, 10, 3, 4, 5, 11, 10, 11, 20]，将其排列成一个新数组，要求新数组形式如下，例如 [[2, 3, 4, 5], [10, 11], [20]]

> > >

```js
// 得到一个两数之间的随机整数，包括两个数在内
function getRandomIntInclusive(min, max) {
  min = Math.ceil(min);
  max = Math.floor(max);
  return Math.floor(Math.random() * (max - min + 1)) + min; //含最大值，含最小值
}
// 随机生成 10 个整数数组, 排序, 去重
let initArr = Array.from({ length: 10 }, (v) => {
  return getRandomIntInclusive(0, 99);
});
initArr.sort((a, b) => {
  return a - b;
});
initArr = [...new Set(initArr)];

// 放入 hash 表
let obj = {};
initArr.map((i) => {
  const intNum = Math.floor(i / 10);
  if (!obj[intNum]) obj[intNum] = [];
  obj[intNum].push(i);
});

// 输出结果
const resArr = [];
for (let i in obj) {
  resArr.push(obj[i]);
}
console.log(resArr);
```

Ref.: [第 67 题：随机生成一个长度为 10 的整数类型的数组，例如 [2, 10, 3, 4, 5, 11, 10, 11, 20]，将其排列成一个新数组，要求新数组形式如下，例如 [[2, 3, 4, 5], [10, 11], [20]]](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/113)

> > >

---

## This

### call

### apply

### bind

---

## Function

### Currying

```js

```

Ref.[高频前端面试题汇总之手写代码篇](https://juejin.cn/post/6946136940164939813#heading-12)

---

## Async

> > >

```js
const list = [1, 2, 3];
const square = (num) => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(num * num);
    }, 1000);
  });
};

function test() {
  list.forEach(async (x) => {
    const res = await square(x);
    console.log(res);
  });
}
test();
```

Ref.[第 160 题：输出以下代码运行结果，为什么？如果希望每隔 1s 输出一个结果，应该如何改造？注意不可改动 square 方法](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/389)

> > >

---

## Class

### 要求设计 LazyMan 类，实现以下功能

> > >

```js
LazyMan("Tony");
// Hi I am Tony

LazyMan("Tony").sleep(10).eat("lunch");
// Hi I am Tony
// 等待了10秒...
// I am eating lunch

LazyMan("Tony").eat("lunch").sleep(10).eat("dinner");
// Hi I am Tony
// I am eating lunch
// 等待了10秒...
// I am eating diner

LazyMan("Tony")
  .eat("lunch")
  .eat("dinner")
  .sleepFirst(5)
  .sleep(10)
  .eat("junk food");
// Hi I am Tony
// 等待了5秒...
// I am eating lunch
// I am eating dinner
// 等待了10秒...
// I am eating junk food
```

Ref.: [第 56 题：要求设计 LazyMan 类，实现以下功能](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/98)

> > >
