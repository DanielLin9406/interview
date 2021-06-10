# Coding

## Index of Contents

### 随机生成一个长度为 10 的整数类型的数组，例如 [2, 10, 3, 4, 5, 11, 10, 11, 20]，将其排列成一个新数组，要求新数组形式如下，例如 [[2, 3, 4, 5], [10, 11], [20]]

> > >

```
 // 得到一个两数之间的随机整数，包括两个数在内
 function getRandomIntInclusive(min, max) {
    min = Math.ceil(min);
    max = Math.floor(max);
    return Math.floor(Math.random() * (max - min + 1)) + min; //含最大值，含最小值
}
// 随机生成 10 个整数数组, 排序, 去重
let initArr = Array.from({ length: 10 }, (v) => { return getRandomIntInclusive(0, 99) });
initArr.sort((a,b) => { return a - b });
initArr = [...(new Set(initArr))];

// 放入 hash 表
let obj = {};
initArr.map((i) => {
const intNum = Math.floor(i/10);
if (!obj[intNum]) obj[intNum] = [];
obj[intNum].push(i);
})

// 输出结果
const resArr = [];
for(let i in obj) {
resArr.push(obj[i]);
}
console.log(resArr);

```

Ref.: [第 67 题：随机生成一个长度为 10 的整数类型的数组，例如 [2, 10, 3, 4, 5, 11, 10, 11, 20]，将其排列成一个新数组，要求新数组形式如下，例如 [[2, 3, 4, 5], [10, 11], [20]]](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/113)

> > >

### 要求设计 LazyMan 类，实现以下功能

> > >

```
LazyMan('Tony');
// Hi I am Tony

LazyMan('Tony').sleep(10).eat('lunch');
// Hi I am Tony
// 等待了10秒...
// I am eating lunch

LazyMan('Tony').eat('lunch').sleep(10).eat('dinner');
// Hi I am Tony
// I am eating lunch
// 等待了10秒...
// I am eating diner

LazyMan('Tony').eat('lunch').eat('dinner').sleepFirst(5).sleep(10).eat('junk food');
// Hi I am Tony
// 等待了5秒...
// I am eating lunch
// I am eating dinner
// 等待了10秒...
// I am eating junk food
```

Ref.: [第 56 题：要求设计 LazyMan 类，实现以下功能](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/98)

> > >

### Array Merge

> > >

Ref.[第 30 题：请把俩个数组 [A1, A2, B1, B2, C1, C2, D1, D2] 和 [A, B, C, D]，合并为 [A1, A2, A, B1, B2, B, C1, C2, C, D1, D2, D]](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/39)

> > >

### Async

> > >

```
const list = [1, 2, 3]
const square = num => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(num * num)
    }, 1000)
  })
}

function test() {
  list.forEach(async x=> {
    const res = await square(x)
    console.log(res)
  })
}
test()
```

Ref.[第 160 题：输出以下代码运行结果，为什么？如果希望每隔 1s 输出一个结果，应该如何改造？注意不可改动 square 方法](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/389)

> > >
