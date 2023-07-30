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
  > The `new.target` meata-property lets you detect whether a function or constructor was called using the `new` operator. In constructors and functions invoked using the `new` operator, `new.target` returns a reference to the constructor or function that new was called upon. In normal function calls, `new.target` is `undefined`.
  
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