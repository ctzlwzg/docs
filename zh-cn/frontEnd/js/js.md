# 常用语法

## 数组

> 数组转字符串,以逗号分隔
```js
//应用场景：后端想以逗号分隔接收，多张图片的地址。
//存储的时候，不一定就先去构建对应的以逗号分隔的字符串，先把得到的图片放在数组中，这样的操作比字符串轻松的多。
arr.join(',');
```

> 删除数组中某一个元素
```js
arr.splice(index,1);//index指的是要删除数组的下标 1，指的是删除的数量
```

> 对象的深拷贝，生成新的对象
```js
JSON.parse(JSON.stringify(obj));// 一般情况下都可以使用
```

> 过滤得到想要的数据
```js
//过滤选中的数据
arr.filter((item) => {
    return item.select;
});
//简写
arr.filter((item) => item.select);
```

> 使用map 会返回新数组，内容是你需要的数据
```js
//对象中cat_id字段改成id字段，cat_name字段改成name字段，并且过滤掉了其他所有的字段，并返回新的数组（一般用于相应的数据，并组装成自己想要的数据）
arr.map(item => {
    return {
        id: item.cat_id,
        name: item.cat_name
    }
})
//直接返回名字，如['鞋子','袜子','裤子','衣服']
arr.map(item => item.cat_name)
```

> ~~使用 扩展运算符(对应实例用法已废弃)~~
```js
//实例:移动端下滑加载更多数据的时候，把新加载出来的数据，添加到goodsList的数组的后面
// 利用扩展运算符 得到数组中所有的数据，然后在放到新的数组中组装得到想要的数据
this.goodsList = [...this.goodsList, ...res.data.list];
```

> ~~使用数组中的concat方法，合并数组(对应实例用法已废弃)~~
```js
//此方法和上面使用 扩展运算符得到的结果是相同的。这是es5的写法，上面扩展运算符是es6的写法，那么我们还是与时俱进，统一使用扩展运算符的写法
this.goodsList = this.goodsList.concat(res.data.list);
```

> 使用函数的push方法来添加数据 **（推荐）**
```js
this.goodsList.push(...res.data.list);

```

> 判断是否数据是否在数组中
```js
let str = 1;
[0, 1].includes(str) //true
```

## 变量
### var关键字
- var声明作用域
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
- var声明提升
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

### let 声明
```js
if (true) {
    let age = 26;
    console.log(age); // 26
}
console.log(age); // ReferenceError: age 没有定义
// 此时这样写就会报错了
```
> 原因：let声明的范围是**块作用域**

### const 声明

## 字符串
> 字符串转数组，通过逗号截取
```js
//应用场景：后端返回图片是以逗号分隔的
str.split(',');
```


## 运算

> 字符串转数字
```js
let str = '111';
let num = +str; // 推荐
// 其他用法
let num = Number(str); // 之间用的多
```