## this

`this`的值取决于函数的调用方式，跟作用域无关哦。  
有四种不同的类型，优先级也基本是这个顺序：

1. 以 `new` 函数构造调用的方式，`this`指向新创建的对象
2. `call/apply`方式，把`this`绑定到指定的上下文（函数的第一个参数），会立即执行；`bind`也是给函数绑定`this`，但不会执行，函数调用时候才会生效
3. 当作为**对象的属性**的形式调用，`this`指向该对象
4. 其他以非箭头函数形式调用，指向`window`--默认调用
5. 箭头函数，本身没有`this`,`this`指向父层第一个非箭头函数的函数的`this`

### you don't know js

#### 为什么需要 this

this 实现了隐式传递一个对象，根据不同上下文函数产生不同的结果，使得 API 的设计更加简洁优雅。

#### 调用位置

此处的调用位置是对应定义位置的，因为`this`是运行时绑定的，所以我们要观察函数调用的地方而不是定义的地方。

#### 绑定规则

1. 非严格模式下，默认指向`window`。是不是严格模式，要看`this`所处的作用域是不是在严格模式，eg:

```js
function foo() {
  console.log(this.a)
}
var a = 2
;(function () {
  'use strict'
  foo()
  // 2
})
```

2. 隐式绑定

以对象的方法的方式调用，`this`被隐式绑定到对象上。  
注意会跟着最里层的对象走。比如`a.b.c()`会绑定到`b`上。  
但凡调用的时候，被传递给了其他函数，就很容易丢掉这种绑定。
