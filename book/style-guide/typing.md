# 类型安全

## 入门

1. [TypeScript 在 React 中使用总结](https://juejin.im/post/5bab4d59f265da0aec22629b)

## 常见问题

### 回调函数的参数类型不确定

回调函数的参数类型通常可以通过找到原函数的定义来获得。

```js
interface DoSomethingResult { val: string }
function doSomething(onComplete: (result: DoSomethingResult) => void) {...}

// BEST
function callback(result: DoSomethingResult) {...}
doSomething(callback);

// GOOD
function callback(result: { val: string }) {...}
doSomething(callback);

// BAD
function callback(result: any) {...}
doSomething(callback);
```

React 中常用的 Event 事件类型有

- `ClipboardEvent<T = Element>` 剪贴板事件对象
- `DragEvent<T = Element>` 拖拽事件对象
- `ChangeEvent<T = Element>` Change 事件对象
- `KeyboardEvent<T = Element>` 键盘事件对象
- `MouseEvent<T = Element>` 鼠标事件对象
- `TouchEvent<T = Element>` 触摸事件对象
- `WheelEvent<T = Element>` 滚轮事件对象
- `AnimationEvent<T = Element>` 动画事件对象
- `TransitionEvent<T = Element>` 过渡事件对象

参考：<https://juejin.im/post/5bab4d59f265da0aec22629b#heading-13>

Taro 中的 Event 事件类型主要继承了 `BaseEventOrig`，常见还有

- `ITouchEvent` 触摸事件
