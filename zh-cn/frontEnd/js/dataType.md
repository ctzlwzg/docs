<!-- 数据类型 -->

## 数据类型分类
1. Undefined
2. Null
3. Boolean
4. Number
5. String
6. Symbol
7. Object

## typeof 操作符
typeof 操作符 是用于判断变量的数据类型
> 对一个值使用typeof操作符会返回**字符串**,字符串这三个字很重要

使用该操作符判断一个值只会返回下面7种情况
1. "undefined" 表示值未定义
2. "boolean"   表示值为布尔值
3. "string"    表示值为字符串
4. "number"    表示值为数字
5. "object"    表示值为对象
6. "function"  表示值为函数
7. "symbol"    表示值为符号

!> 注意：返回值是小写的，和数据类型大写有所区别

## Undefined类型
Undefined类型只有一个值，就是特殊值undefined。当使用var或let声明了变量但没有初始化是，就相当于给变量赋予了undefined值。
```js
let aaa;
//let aaa = undefined; 效果和let aaa;相同
console.log(aaa); // 打印undefined
console.log(aaa == undefined); // 打印true
```
!> 注意：不要显式的定义某个变量的值为undefined。字面量undefined主要用于比较。增加这个特殊的值的目的是为了正式明确空对象指针（null）和未初始化变量的区别


- 对于**未初始化**的变量调用typeof时，返回结果是"undefined"

- 对于**未定义**的变量调用typeof时，返回结果还是"undefined"

```js
let aaa;
console.log(typeof(aaa)) // "undefined"
console.log(typeof(bbb)) // "undefined"
```

!> 注意：我们仍然建议在声明变量的同时进行初始化。这样当typeof返回"返回undefined"时，就会知道是给定的变量没有声明，而不是声明了没有使用。即不建议这样写let aaa;建议这样写let aaa = '';

> undefined 是一个假值
```js
let aaa;

if(aaa){
  // 不会执行
}

if(!aaa){
  // 会执行
}

```

## Null类型

Null类型同样只有一个值，即特殊值null。逻辑上讲，null值表示一个空对象的指针，这也是给typeof传递一个null会返回"object"的原因。
```js
let aaa = null;

console.log(typeof(aaa)) // "object"
```

!> 建议：在定义未来要保存对象值的变量时，建议使用null来初始化，而不是其他值，如 let obj = '';不建议。

!> 这样只要检查这个变量的值是不是null就可以知道这个变量是否在后来被重新赋予了一个对象的引用

undefined是有null派生而来的，因此ECMA-262 将它们定义为表面上相等
```js
console.log(undefined == null) // true
```

但他们的用途完全不同，在任何时候，只要变量要保存对象，而当时又没有那个对象可保存，就可以用null来填充改变量。

> null是一个假值
```js
let aaa = null;

if(aaa){
  // 不会执行
}

if(!aaa){
  // 会执行
}
```

