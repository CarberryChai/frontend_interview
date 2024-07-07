# JavaScript
## 1. 写一个构造函数，实现new和直接调用一样效果
```js
  function Test() {
    this.a = 1
    this.b = function() {
      console.log('hello world')
    }
  }
  const t1 = new Test() // t1 Test{a:1, b: function(){}}
  const t2 = Test() // t2 Test{a:1, b: function(){}}
```
* 考察[`new`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/new) 关键字
  > If the constructor function returns a non-primitive, this return value becomes the result of the whole `new` expression. Otherwise, if the constructor function doesn't return anything or returns a primitive, `newInstance` is returned instead. (Normally constructors don't return a value, but they can choose to do so to override the normal object creation process.)

  > `Classes` can only be instantiated with the `new` operator -- attempting to call a class without `new` will throw a `TypeError`.

* `new.target`
  > The `new.target` meta-property lets you detect whether a function or constructor was called using the `new` operator. In constructors and functions invoked using the `new` operator, `new.target` returns a reference to the constructor or function that new was called upon. In normal function calls, `new.target` is `undefined`.
  
```js
  function Test() {
    if(!new.target) {
      return new Test()
    }
    this.a = 1
    this.b = function() {
      console.log('hello world')
    }
  }
```
## 2. Map和Set的区别，Map和Object的区别
`Map`是一个键值对的集合，其中的键可以是任何类型。`Set`是一组值的集合，其中的值是唯一的，没有重复值。`Map`和`Set`都会记录值的插入顺序，能够根据插入顺序进行迭代。

`Map`允许任何类型的键，包括对象、函数、原始数据类型等，`Object`的键必须是字符串或符号（Symbol）,其他类型的键会被自动转换为字符串。`Object` 存在原型链，可能会与对象原型链上的键发生冲突
## 3. 了解事件循环机制吗？
JS 中的事件循环（Event Loop）是一种用于管理和调度异步任务执行的机制。它使得 JS 可以处理异步操作，如定时器、事件处理、网络请求等，而不会阻塞主线程的执行。
## 4. 说一下什么是宏任务微任务，为什么要定义这两种任务类型？
宏任务（macro tasks）和微任务（micro tasks）是 JavaScript 引擎中用于管理异步任务执行顺序的两种任务类型。

**宏任务**（Macro Tasks）：是指那些需要在主线程中执行的任务，包括但不限于：
- 定时器任务（Timers）：通过 `setTimeout`、`setInterval`创建的任务。
- I/O 操作任务： 例如文件读写、网络请求等异步任务。
- 渲染事件（UI Rendering）：处理用户交互事件（例如鼠标点击、键盘事件等）的任务。
- 事件处理器任务（Event Handlers）：事件监听器、事件回调等。
**微任务（Micro Tasks）** ：是指在当前任务执行完成后立即执行的任务，它们包括：
- Promise 回调：使用 Promise 对象的 then 方法添加的回调函数。
- `MutationObserver`回调：通过`MutationObserver`观察 DOM 变化并触发的任务。
- `process.nextTick`（在 Node.js环境中）：在事件循环的当前回合结束时执行的任务。

**宏任务和微任务的引入使得 JavaScript 引擎能够很好的处理异步任务。**

宏任务用于表示一组相对较大的任务单元，而微任务用于表示一组相对较小、优先级较高的任务单元。

通过微任务，我们可以在宏任务执行完成后立即执行一些重要的任务，例如更新 UI、处理 Promise 的回调等，以提高应用的响应速度和用户体验。