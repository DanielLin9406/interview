# Coding

## Index of Contents

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

### Promise

### Promise.then

### Promise.all

### Promise.race

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

Ref.[第 30 题：请把俩个数组 [A1, A2, B1, B2, C1, C2, D1, D2] 和 [A, B, C, D]，合并为 [A1, A2, A, B1, B2, B, C1, C2, C, D1, D2, D]](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/39)

> > >

### Async

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
