<!-- 变量 -->
## var关键字
> var声明作用域
```js
function test() {
    var message = "hi"; // 局部变量
}
test();
console.log(message); // 出错！
function test() {
    message = "hi"; // 全局变量
}
test();
console.log(message); // "hi"
```
> var声明提升
```js
function foo() {
    console.log(age);
    var age = 26;
}
foo(); 
// 打印 undefined
// 即
function foo() {
    var age;
    console.log(age);
    age = 26;
}
foo();
// 打印 undefined
```

> 之所以不会报错，是因为ECMAScript运行时age变量声明会提升到**函数作用域**的顶部
```js
if (true) {
    var name = 'Matt';
    console.log(name); // Matt
}
console.log(name); // Matt
```
> var 声明的范围是函数作用域，所以在if作用域的声明的变量，在外面可以获取到

> **函数作用域** 这几个很字重要，这一特性就是和let const关键字声明变量的区别

## let 声明
> let声明的范围是**块作用域**，块作用域是函数作用域的子集，那么适用于var的作用域限制同样也适用于let
```js
if (true) {
    let age = 26;
    console.log(age); // 26
}
console.log(age); // ReferenceError: age 没有定义
// 此时这样写就会报错了
```


> 同一个**块作用域**中出现的变量声明是不允许的，会报错
```js
let a;
let a;//SyntaxError；标识符 a 已经声明过了
// Uncaught SyntaxError: Identifier 'a' has already been declared
```
> 暂时性死区：即let声明的变量不会进行类似var声明的提升。在let声明之前的执行瞬间被称为“暂时性死区”
```js
// age 不会被提升
console.log(age); // ReferenceError： age 没有定义
let age = 26;
```
## const 声明
> const声明变量时必须同时初始化变量，且不能修改
> 但const变量的引用是一个对象，那么修改这个对象内部的属性是可以的
```js
const person = {};
person.name = '吴正刚';//不会报错
```

> const声明不能用来声明迭代变量，原因也很明显，迭代变量会变化---自增，自减等
```js
for (const i = 0; i < 10; ++i) {} // TypeError：给常量赋值
```
> 但在forin,forof 循环中可以使用，原因：每次迭代创建了一个新的变量
```js
for (const key in {a: 1, b: 2}) {
console.log(key);
}
// a, b
for (const value of [1,2,3,4,5]) {
console.log(value);
}
// 1, 2, 3, 4, 5
```

!> 不使用var
> 先使用const ,let次之

!> 在严格模式下有些代码会报错，需注意。如使用vite来做开发服务器，默认是严格模式的。