# Optimization

## Index of Contents

- Throttle

```js
function throttle(fn) {
  let canRun = true;
  return function () {
    if (!canRun) return;
    canRun = false;
    setTimeout(() => {
      fn.apply(this, arguments);
      canRun = true;
    }, 500);
  };
}
function sayHi(e) {
  console.log(e.target.innerWidth, e.target.innerHeight);
}
window.addEventListener("resize", throttle(sayHi));
```

Ref.[Throttle](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/5)

- Debounce

```js
function debounce(fn) {
  let timeout = null;
  return function () {
    clearTimeout(timeout);

    timeout = setTimeout(() => {
      fn.apply(this, arguments);
    }, 500);
  };
}
function sayHi() {
  console.log("防抖成功");
}

var inp = document.getElementById("inp");
inp.addEventListener("input", debounce(sayHi));
```

Ref.[debounce](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/5)

- Endless Carousel
