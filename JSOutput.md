# Javascript Output

## Index of Topic

- What is the output?

## What is the output

### Hoisting

```
var b = 10;
(function b() {
  b = 20;
  console.log(b)
})()
```

> 声明提前：一个声明在函数体内都是可见的，函数声明优先于变量声明；在非匿名自执行函数中，函数变量为只读状态无法修改
> Ref.: [第 33 题：下面的代码打印什么内容，为什么？](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/48)

### Hoisting and Assign Value

> > >

```
var a = 10;
(function () {
    console.log(a)
    a = 5
    console.log(window.a)
    var a = 20;
    console.log(a)
})()
```

Ref.[第 41 题：考察作用域的一道代码题
](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/61)

> > >

### Radix

```
['1', '2', '3'].map(parseInt)
```

- ParseInt (string, radix)
- Radix is between 2-36

#### Read More

> ['10','10','10','10','10'].map(Number);
> // [10, 10, 10, 10, 10]

> > > Ref. [第 2 题：['1', '2', '3'].map(parseInt) what & why ?](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/4)

### Hidden Type Conversion

> > >

```
var a = ?;
if(a == 1 && a == 2 && a == 3){
 	conso.log(1);
}
```

Ref.: [第 38 题：下面代码中 a 在什么情况下会打印 1？](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/57)

> > >

### Async

> > >

```
const promise = new Promise((resolve, reject) => {
  console.log(1);
  resolve(5);
  console.log(2);
}).then(val => {
  console.log(val);
});

promise.then(() => {
  console.log(3);
});

console.log(4);

setTimeout(function() {
  console.log(6);
});

```

Ref. [第 13 题：Promise 构造函数是同步执行还是异步执行，那么 then 方法呢？](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/19)

> > >
