## new

1. `new` 不是构造函数的调用方式，所有的函数都可以通过它实现**构造调用**
   使用`new`创建对象会产生的过程：

- 创建一个新对象
- 链接原型
- `this`指向该对象，执行函数
- return 指定值，如果没有指定，则返回`this`

模拟一下

```js
function createObj() {
  const obj = {}
  obj.__proto__ = arguments.callee.prototype
  const res = createObj.call(obj, arguments)
  return res
}
```

2. 优先级

```js
function d() {
  console.log(1)
}
d.fun = function () {
  console.log(2)
}
d.prototype.fun = () => {
  console.log(3)
}
new d().fun()
// 1
// 3
// 等价于 (new d()).fun()
new d.fun()
// 2
// 等价于 new (d.fun())
```
