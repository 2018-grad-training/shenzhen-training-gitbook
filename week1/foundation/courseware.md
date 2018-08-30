## Javascript引言

### 什么是JavaScript？

JavaScript 是一门跨平台、面向对象的轻量级脚本语言，它也是一门动态编程语言。

### 为什么使用JavaScript？

* 客户端
* 服务器

### JavaScript历史

* 1995年诞生，运行于网景 Navigator2 浏览器中
* ECMAScript 是下一代 JavaScript 语言
  * ES3\(1999\)
  * ES4 abandoned
  * ES5\(2009\)
  * ES6/ES2015，ES2016，ES2017，ES2018…
* TypeScript 是JavaScript的超集

### Javascript运行环境

* Web控制台
* node运行环境
* node工程 https://github.com/2018-grad-training/tw-js-scaffold
* Javascript在线编辑器 http://jsbin.com/

## Javascript语法

### 变量声明

* var

  声明一个变量，可赋一个初始化值。

* let

  声明一个块作用域的局部变量，可赋一个初始化值。

* const

  声明一个块作用域的只读的命名常量。

### 注释

```javascript
// 单行注释 常用

/* 这是一个更长的,
   多行注释
*/
```

### 日志和调试

* 日志

  * console.log\(\)
  * console.info\(\)
  * console.error\(\)

* 调试

  * console.log\(\)
  * debugger;
  * 浏览器内置的调试器

## Javascript语法和类型

Javascript中值是有类型的，变量是没有类型的。

### 原型数据类型

* Boolean.  布尔值，true 和 false.
* Number.  表示数字，例如： 42 或者 3.14159。
* String.  表示字符串，例如："Howdy"
* null
* undefined

### 内置对象类型

Javascript中除了原型数据类型，其他所有值都是对象。原型数据类型是不可变的，Javascript中的对象是可变的键控集合。

* Function 
* Object 
* Array
* Number对象 
* String对象 
* Boolean对象

JS提供的对象方法绑定在prototype上，ES6对prototype方法进行了扩展。

#### Object

[https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global\_Objects/Object](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object)

* 检索：obj\[prop\], obj.prop, Object.hasOwnProperty\(\), Object.defineProperty\(\) ...
* 构造：Object.create\(\), Object.assign\(\)
* 枚举：for in
* 遍历：Object.keys\(\), Object.values\(\), Object.entries\(\)

#### Array

[https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global\_Objects/Array](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array)

* 构造：Array.from\(\), Array.of\(\)
* 遍历：Array.map\(\), Array.forEach\(\), Array.filter\(\), Array.reduce\(\), Array.find\(\) ...
* 枚举：for, for in, for of
* 元素：Array.pop\(\), Array.push\(\), Array.shift\(\), Array.unshift\(\), Array.splice\(\), Array.slice\(\) ... 
* 集合：Array.concat\(\), Array.join\(\) ... 

#### String对象

* 构造：new String\(\)
* 方法：split/match/replace/substring
* 模板字符串：
  ```javascript
  let name = "Bob";
  console.log(`Hello ${name}`);
  ```

#### Number对象

* 构造：new Number\(\)
* 方法：Number.isFinite\(\), Number.isNaN\(\), Number.parseInt\(\), Number.parseFloat\(\), Number.isInteger\(\) ...

#### Boolean对象

* 构造：new Boolean\(\)
* 基本类型中的布尔值true/false与值为true/false的Boolean对象不同
  ```javascript
  var x = new Boolean(false);
  if (x) {
  // 这里的代码会被执行
  }
  ```

### 强制转换

**显式强制转换**

* Number\(foo\), String\(foo\), Boolean\(foo\)
* +foo
* foo.toString\(\)
* !!foo

**隐式强制转换**

* foo + "", foo - ""
* if\(foo\){}
* ==

#### Falsy值
false, 0, "", null, undefined, NaN

## 分支和循环

### 分支

* if...else
* switch
* try/catch/throw

### 循环

* for
* while
* do...while
* break/continue
* for..in
* for..of

for...in循环出的是key，for...of循环出的是value。推荐在循环对象属性的时候，使用for...in,在遍历数组的时候的时候使用for...of

## 函数

### 函数定义

* 函数就是对象，因此可以像任何其他值一样被使用
* 函数是一等公民
  * 函数可以作为参数传给其他函数
  * 函数能够被返回
  * 函数可以保存在变量、对象或数组中
* 函数可以被调用

### 函数作用域

函数中的参数和变量在函数外部不可见，而在函数内部任何位置定义的变量，在该函数内部都可见。

```javascript
function diff(x, y) {
  if (x > y) {
    var temp = x;
    x = y;
    y = temp;
  }
  return y - x;
}
```
temp是函数作用域，如果用let声明temp，则具有了块级作用域

### 函数调用

调用模式不同在初始化this上存在差异

#### 方法调用模式

函数作为对象的属性时，被成为方法。方法调用时，this绑定到该对象上

```javascript
const myObject = {
  value: 1,
  increment: function() {
    this.value += 1;
  }
};
myObject.increment();
```

#### 函数调用模式

函数也可以直接被调用，此时this绑定到全局对象。

```javascript
function makeNoSense(x) { 
  this.x = x; 
} 
makeNoSense(5); 
console.log(x);
```

声明在另外一个函数体内的函数，这种绑定到全局对象的方式会产生问题。

```javascript
const point = { 
  x: 0, 
  moveTo : function(x) { 
    const moveX = function(x) { 
      this.x = x;
    }; 
    moveX(x); 
  } 
}; 
point.moveTo(1);
console.log(point.x, x);
```

```javascript
const point = { 
  x: 0, 
  moveTo : function(x) {
    const that = this;
    const moveX = function(x) { 
      that.x = x;
    }; 
    moveX(x); 
  } 
}; 
point.moveTo(1);
console.log(point.x);
```

#### 构造函数调用模式

采用new来调用，会创建一个新对象，同时this会绑定到这个新对象上。

```javascript
function Point(x, y){ 
   this.x = x; 
   this.y = y; 
}
new Point(1,2);
```

#### 使用apply或call调用模式

```javascript
function Point(x){ 
   this.x = x; 
   this.moveTo = function(x){ 
       this.x = x; 
   } 
} 

var p1 = new Point(0); 
var p2 = {x: 0}; 
p1.moveTo(1); 
p1.moveTo.apply(p2, [10]);
```

apply和call允许切换函数执行的上下文环境，即this绑定的对象。

### 箭头函数和this

较短的语法并以词法的方式绑定this

```javascript
function Person() {
  this.age = 0;

  setTimeout(function growUp() {
    this.age++;
    console.log(this.age);
  }, 1000);
}

var p = new Person();
```

```javascript
function Person(){
  this.age = 0;

  setInterval(() => {
    this.age++;
  }, 1000);
}

var p = new Person();
```

### 闭包

#### 闭包的定义

每个函数在创建时会附加两个隐藏属性：函数上下文和实现函数行为的代码。因此当函数嵌套时，内部函数可以访问外部函数的作用域。

```javascript
var pet = function(name) {          //外部函数定义了一个变量"name"
  var getName = function() {            
    return name; 
  }
  return getName;               
};
myPet = pet("Vivie");
myPet();
```

#### 闭包的用途

```javascript
var names = ['zero', 'one', 'two', 'three', 'four', 'five', 'six', 'seven', 'eight', 'nine'];
var digit_name = function (n) {
    return names[n];
};
```

```javascript
var digit_name = function (n) { 
    var names = ['zero', 'one', 'two', 'three', 'four', 'five', 'six', 'seven', 'eight', 'nine'];
    return names[n];
};
```

```javascript
var digit_name = (function () {
    var names = ['zero', 'one', 'two', 'three', 'four', 'five', 'six', 'seven', 'eight', 'nine'];
    return function (n) {
        return names[n];
    };
}());
```

## Promise

### 回调

把函数作为参数传入到另一个函数中。这个函数就是所谓的回调函数。JavaScript 的回调是在异步调用场景下使用的。

```javascript
var func1 = function(callback){  
    callback();  
}
```

### Promise

Promise，简单说就是一个容器，里面保存着某个未来才会结束的事件（通常是一个异步操作）的结果。  
Promise对象代表一个异步操作，有三种状态：pending（进行中）、fulfilled（已成功）和rejected（已失败）。

```javascript
const promise = new Promise(function(resolve, reject) {
  if (/* 异步操作成功 */){
    resolve(value);
  } else {
    reject(error);
  }
});
```

## NodeJS模块

### npm新建工程

新建工程:

```
npm init
```

安装npm包:

```
npm install --save colors
```

启动工程：

```
node index.js
```

### npm工程介绍

package.json

```json
{
  "name": "test",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC",
  "dependencies": {
    "colors": "^1.3.1"
  }
}
```

### 模块导入和导出

模块导入:

```javascript
const colors = require("colors");
```

模块导出:

```javascript
module.exports = function log(a) {
  console.log(a);
}
```

ES6模块导入:

```javascript
import {colors} from 'colors';
```

ES6模块导出:

```javascript
export default function log(a) {
  console.log(a);  
}
```



