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
> 对一个值使用typeof操作符会返回`字符串`,字符串这三个字很重要

使用该操作符判断一个值只会返回下面7种情况
1. "undefined" 表示值未定义
2. "boolean"   表示值为布尔值
3. "string"    表示值为字符串
4. "number"    表示值为数字
5. "object"    表示值为对象
6. "function"  表示值为函数
7. "symbol"    表示值为符号

!> 注意：返回值是小写的，且都是`字符串`。它和数据类型大写有所区别。

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

> undefined 是一个`假值`
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

> null是一个`假值`
```js
let aaa = null;

if(aaa){
  // 不会执行
}

if(!aaa){
  // 会执行
}
```

## Boolean类型
Boolean(布尔值)类型有两个字面量：true和false。

虽然布尔值只有两个，但其他类型的值都有相应布尔值的等价形式。
要将一个其他类型的值转换为布尔值，可以调用Boolean()转型函数

下表是不同类型与布尔值之间的转换规则

| 数据类型 | 转换为true的值 | 转换为false的值 |
| :----:  | :----: | :----: |
| Boolean | true | false |
| String | 非空字符串 | ""(空字符串) |
| Number | 非零数值(包括无穷值) | 0、NaN |
| Object | 非null对象 | null |
| Undefined | 不存在 | undefined |

!> 记住这些转换规则，后续会使用到的


## Number类型
Number类型表示整数和浮点值

Infinity 表示正无穷大，-Infinity 表示负无穷大



> `NaN`: "不是数值" （not a Number），用于表示本来要返回数值的操作失败了（而不是抛出错误）
```js
console.log(0/0); // 打印 NaN
console.log(1/0); // 打印 Infinity
console.log(1/-0); // 打印 -Infinity
```

NaN的特性：
1. 任何涉及NaN的操作始终返回NaN（NaN / 1）
2. NaN不等于包括NaN在内的任何值
  ```js
  console.log(NaN == NaN); // false
  ```
  因为特性二，ECMAScript提供了isNaN的函数。该函数接收一个参数，参数是任意类型的，然后判断是否"不是数字"，用于解决判断是否NaN的问题。

`isNaN`的使用：
```js
console.log(isNaN(NaN));// true
console.log(isNaN(1)); // false
console.log(isNaN('1'));//false，隐式类型转换位数字1
console.log(isNaN(false));//fasle,隐式类型转换位数字0
console.log(isNaN(true));//false，隐式类型转换位数字0

console.log(isNaN('wzg'));//true,不可以转换为数值
```
其中涉及到了隐式类型转换，即在做isNaN判断的时候，会对数据进行隐式的（自动的）数值转换操作，Number(xxx)，后面详细介绍

`数值转换`有 3 个函数可以将非数值转换为数值
1. Number()：可用于任何数据类型
2. parseInt()：主要用于将字符串转换为数值。
3. parseFloat()：主要用于将字符串转换为数值。

`Number()`函数的转换规则
1. 布尔值，true转换为1，false转换为0
2. 数值，直接返回
3. null 返回 0
4. undefined 返回NaN
5. 字符串，分下面5种情况
  - 如果是空字符串，返回0
  - 如果 字符串中包含数值字符，包括数值字符**前**面带上 `+`,`-` 的情况，则转换为一个十进制数值。举例：
    - Number('123')返回123
    - Number('+123')返回123
    - Number('-123')返回-123
    - Number('0123')返回123（会忽略前面的0）
  - 如果字符串包含浮点格式，则会转换为相应的浮点值（会忽略前面的0）,包括数值字符**前**面带上 `+`,`-` 的情况，举例：
    - Number('1.23')返回1.23
    - Number('+1.23')返回1.23
    - Number('-1.23')返回-1.23
    - Number('01.23')返回1.23
    - Number('1.23.1')返回NaN,这不是浮点格式
  - 如果字符串包含有效的十六进制格式，会转换为对应的十进制整数值
    - Number("0xf") 返回15
  - 如果字符串包含除上述情况之外的其他字符，返回 NaN
6. 对象,~~调用 valueOf()方法，并按照上述规则转换返回的值。如果转换结果是 NaN，则调用
toString()方法，再按照转换字符串的规则转换。~~(没看懂，我测试了下都是NaN)

`parseInt()`函数更加专注于字符串是否包含数值模式。规则：
 - 字符串前面的空格会被忽略，从第一个非空格字符串开始转换。如果第一个字符不是`数值字符`、`+`、`-`，返回NaN，这意味着空字符串也会返回NaN。
 - 如果第一个字符是`数值字符`、`+`、`-`，继续依次检查每个字符，直到字符串末尾，或碰到非数值字符

```js
  parseInt("1234blue"); // 1234
  parseInt(""); // NaN
  parseInt("22.5");//22
  parseInt("22.5.2");//22
```
`parseInt()`中第二个参数指定底数（进制数），转换为对应的十进制数
```js
let num = parseInt("0xAF", 16); // 175
let num1 = parseInt("10", ''); // 2，
let num1 = parseInt("10", false); // 2，
let num1 = parseInt("10", undefined); // 2，
let num1 = parseInt("10", null); // 2，
let num1 = parseInt("10", 0); // 2，按二进制解析
let num1 = parseInt("10", 1); // NaN
let num1 = parseInt("10", 2); // 2，按二进制解析
let num2 = parseInt("10", 8); // 8，按八进制解析
let num3 = parseInt("10", 10); // 10，按十进制解析
let num4 = parseInt("10", 16); // 16，按十六进制解析
```
!> 进制参数必须在2到36之间，但如果进制0，undefined，null，false默认还是十进制。这里和toString()方法转进制不同（只能2-36）

!> 如果指定的进制不对,或者数据无法转换为对应的进制，都返回NaN。


`parseFloat()`  xxx

## String类型
String（字符串）可以使用双引号，单引号，反引号表示

字符串的特点：一旦创建，它的值就是`不可变的`

`toString()`方法，用于把一个值转换为字符串
```js
let aaa = 1;
aaa.toString();// '1' 变成字符串1
```

但是对于 null 或者undefined 调用toString方法的话，会报错无法读取属性。

`VM61874:1 Uncaught TypeError: Cannot read properties of undefined (reading 'toString')`

`VM61955:1 Uncaught TypeError: Cannot read properties of null (reading 'toString')`

所以就有了第二种转化字符串的方法`String()`
```js
String(null); // 'null'
String(undefined); // 'undefined'
```

`toString()`方法还可以传参，可以得到数值的二进制，八进制，十六进制或者其他进制的字符串
```js
let num = 20;
num.toString();// '20'
num.toString(2);//'10100'
num.toString(8);//'24'
num.toString(16);//'14'

//如果 num不是Number类型，toString函数传参是无效的
```

`字符串插值`
```js
let num = 10;
let str = `苹果的数量有${10}个`;
```
> 在插值表达式中可以调用函数和方法
```js
function getNum(){
  return 10;
}
let str = `苹果的数量有${getNum()}个`;
```

## Symbol类型
 // 内容很多，暂时可以不了解（主要目前我还没有在实际生产中用到）

  代表唯一的，不可变的基本数据类型。【目的】是保证对象属性的唯一性，也是为了解决属性冲突。

 ```js
  let sym1 = Symbol('a');
  let sym2 = Symbol('a');
  console.log(sym1 === sym2); // false

 ```

##### 例1：
在新增多规格（多个规格名称和多个规格值）的时候，需要创建规格对应的列表，此时每一条数据都需要一个唯一的标识，以前通过时间戳来创建唯一标识id,可能会相同，我换了一个做法，每次创建的时候，延时几十毫秒来解决问题。有了Symbol类型，可以解决这个问题，因为Symbol类型是唯一的，不会重复。

##### 例2：
在[原型与原型链](zh-cn/frontEnd/js/原型与原型链.md?id=实现call函数) 那节中，手写call函数中运用到了Symbol，可以解决创建属性的时候，属性名重复的问题。

## Object类型
后面再介绍
