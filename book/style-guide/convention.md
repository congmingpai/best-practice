# 代码准则

## 通用

### Early Return

当一个函数已经可以得到计算结果时，尽可能早的返回。

```js
// GOOD
() => {
  const a = checkA();
  if (!a) {
    return;
  }

  const b = checkB();
  if (!b) {
    return;
  }

  ...
}

// BAD
() => {
  const a = checkA();
  if (a) {
    const b = checkB();
    if (b) {
      const c = checkC();
      if (c) {
        ...
      }
    }
  }
}
```

### 纯函数 Pure function

相同的输入，永远会得到相同的输出，而且没有任何可观察的副作用，即为纯函数。

纯函数的好处是：

1. 可移植/可复用
1. 可测试
1. 可缓存
1. 可替换

参考：[纯函数的好处](https://llh911001.gitbooks.io/mostly-adequate-guide-chinese/content/ch3.html)

```js
// GOOD
function plus(a, b) {
  return a + b;
}
const c = plus(1, 2);
console.log(c);

// BAD1：函数有副作用（修改了外部状态），不是纯函数
let c = 0;
function plusWithSideEffect(a, b) {
  c = a + b;
}
plusWithSideEffect(1, 2);
console.log(c);

// BAD2：函数依赖于外部状态，输入
let b = 2;
function plusNotPure(a) {
  return a + b;
}
const c = plusNotPure(1);
console.log(c);
```
