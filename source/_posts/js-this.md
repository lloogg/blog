---
title: js-this
date: 2022-04-27 14:19:06
tags:
---

this 实际上是在函数被调用时发生的绑定，它指向什么完全取决于函数在哪里被调用。

## this 绑定规则

### 默认绑定

```js
var a = 1;
function foo() {
  console.log(this.a);
}
foo(); // 1
```

调用 foo 时使用了**默认绑定**，this 指向全局对象

### 隐式绑定

```js
function foo() {
  console.log(this.a);
}
var obj = {
  a: 2,
  foo: foo,
};
obj.foo(); // 2
```

当函数引用有上下文对象时，隐式绑定规则会把函数调用中的 this 绑定到这个上下文对象。

对象属性引用链中只有最顶层或者说**最后一层**会影响调用位置。

```js
function foo() {
  console.log(this.a);
}
var obj2 = {
  a: 42,
  foo: foo,
};
var obj1 = {
  a: 2,
  obj2: obj2,
};
obj1.obj2.foo(); // 42
```

#### 隐式丢失

一个最常见的 this 绑定问题就是被隐式绑定的函数会丢失绑定对象，也就是说它会应用默认绑定，从而把 this 绑定到全局对象或者 undefined 上，取决于是否是严格模式。

```js
function foo() {
  console.log(this.a);
}
var obj = {
  a: 2,
  foo: foo,
};
var bar = obj.foo; // 函数别名！
var a = 'oops, global'; // a 是全局对象的属性
bar(); // "oops, global"
```

### 显式绑定

#### 1. 硬绑定

call，apply，bind

#### 2. Api 的引用上下文

```js
function foo(el) {
  console.log(el, this.id);
}
var obj = { id: 'awesome' }; // 调用 foo(..) 时把 this 绑定到 obj [1, 2, 3].forEach( foo, obj ); // 1 awesome 2 awesome 3 awesome
```

实际就是通过 call，apply 实现了显示绑定

### new 绑定

所有函数都可以通过
this 实际上是在函数**被调用时**发生的绑定，它指向什么**完全取决于函数在哪里被调用**。

## 默认绑定

## 隐式绑定

### 隐式绑定丢失

一个最常见的 this 绑定问题就是被隐式绑定的函数会丢失绑定对象，也就是说它会应用默认绑定，从而把 this 绑定到全局对象或者 undefined 上，取决于是否是严格模式。
