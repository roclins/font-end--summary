# 一文看懂 yield 

## 总结

- next（）函数会使 Generator函数继续执行下去，直至碰到下一个 yield 语句，yield 的expression 会作为 next（）的输出，然后，函数就此暂停；直到新的next（a）函数出现，此时的 yield 语句（也就是刚刚那一暂停的那个）的 cv 接收参数 a ，函数恢复执行，直到碰到一下 yield 语句。。。。。。
- yield 语句返回的是一个对象，{ value：expression，done：false/true },碰到 yield 时，done 为 false ，return 为 true。

## Generator

Generator 函数是协程在 ES6 的实现，最大的特点就是交出函数的执行权（暂停执行）

一个 Generator 与普通 function 函数的最大区别在于函数名前面多了一个*，但是执行时有很大的不同，与 yield 语句配合，可以实现函数暂时执行的功能

## yield 

### 语法 

```
[rv] = yield [expression];
```

### 描述

`yield`关键字使生成器函数执行暂停，`yield`关键字后面的表达式的值返回给生成器的调用者。它可以被认为是一个基于生成器的版本的`return`关键字。

`yield`关键字实际返回一个`IteratorResult`对象，它有两个属性，`value`和`done`。`value`属性是对`yield`表达式求值的结果，而`done`是`false`，表示生成器函数尚未完全完成。

一旦遇到 `yield` 表达式，生成器的代码将被暂停运行，直到生成器的 `next()` 方法被调用。每次调用生成器的`next()`方法时，生成器都会恢复执行，直到达到以下某个值：

- `yield`，导致生成器再次暂停并返回生成器的新值。 下一次调用`next()`时，在`yield`之后紧接着的语句继续执行。
- [`throw`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/throw)用于从生成器中抛出异常。这让生成器完全停止执行，并在调用者中继续执行，正如通常情况下抛出异常一样。
- 到达生成器函数的结尾；在这种情况下，生成器的执行结束，并且`IteratorResult`给调用者返回[`undefined`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/undefined)并且`done`为`true`。
- 到达[`return`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/return) 语句。在这种情况下，生成器的执行结束，并将`IteratorResult`返回给调用者，其值是由`return`语句指定的，并且`done` 为`true`。

如果将可选值传递给生成器的`next()`方法，则该值将成为生成器当前`yield`操作返回的值。

在生成器的代码路径中的`yield`运算符，以及通过将其传递给[`Generator.prototype.next()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Generator/next)指定新的起始值的能力之间，生成器提供了强大的控制力。

### 示例

```
function *foo(x) {
  let y = 2 * (yield (x + 1))
  let z = yield (y / 3)
  return (x + y + z)
}
let it = foo(5)
console.log(it.next())   // => {value: 6, done: false}
console.log(it.next(12)) // => {value: 8, done: false}
console.log(it.next(13)) // => {value: 42, done: true}
```

### 解析

- `foo（5）`不会输出，说明 `Generator` 函数直接运行时，是不会执行函数体内的代码

- `it.next（）`使得函数开始执行函数体内的代码，直到遇到下一个的 `yield`，也就是

  `let y = 2 * (yield (x + 1))`，此时，`expression （x+1）的结果`作为返回值传递给`it.next（）`，然后函数就此暂停，直到生成器的 `next()` 方法被调用

- `it.next(12)`使得函数继续运行，`12` 作为`yield (x + 1）` 的  `rv` ，所以  `y`等于`24`，

  碰到`let z = yield (y / 3)`,函数暂停，返回值的`value` 为`24/3=8`，返回值是一个对象`{value: 8, done: false}`，函数暂停。

- `it.next(13)`函数继续运行，碰到 `return (x + y + z)`，返回值为

  `{value: 42, done: true}`，此时 `done` 为 ` true`

