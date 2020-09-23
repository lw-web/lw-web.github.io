# JS手写代码

## 防抖节流函数

- 防抖函数

```js
function debounce(fn, wait) {
  let timeout;
  return function () {
    let context = this;
    let args = arguments;

    if (timeout) clearTimeout(timeout);
    timeout = setTimeout(() => {
      fn.apply(context, args);
    }, wait);
  };
}

debounce(() => {
  console.log("函数执行了！");
}, 500);
```

- 节流函数

```js
function throttle(fn, wait) {
  let previous = 0;
  return function () {
    let now = Date.now();
    let context = this;
    let args = arguments;

    if (now - previous > wait) {
      fn.apply(context, args);
      previous = now;
    }
  };
}

throttle(() => {
  console.log("函数执行了！");
}, 500);
```

