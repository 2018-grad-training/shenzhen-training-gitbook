## Javascript OO

### 基于类的面向对象语言

**类**

是定义同一类所有对象的变量和方法的蓝图或原型

**对象**

当创建类的实例时（实例化），就创建了这种类型的一个对象。

通过构造器方法来实例化类。通过 new 操作符创建单个对象。

**继承**

子类将继承父类的全部属性，并可以添加新的属性或者修改继承的属性。

**多态**

子类重写父类的方法

### 基于原型的面向对象语言

**对象**

只有对象！！！一个基于原型的面向对象语言，没有类，只有对象。

- **类意味着复制**
    
    传统的类被实例化时，它的行为会被复制到实例中。类被继承时，行为也会被复制到子类中。
    多态看起来似乎是从子类引用父类，但是本质上引用的其实是复制的结果。
- **对象之间的关系不是复制而是委托**

#### 原型链
JavaScript 中的对象有一个特殊的[[Prototype]] 内置属性，其实就是对于其他对象的引用。
```javascript
var employee = {
  name: "Jane"
};
employee.name;
```
试图引用对象的属性时会触发原型[[Get]] 操作。

```javascript
var employee = {
  name: "Jane"
};
var manager = Object.create( employee );
manager.name;
```
对于默认的[[Get]] 操作来说，如果无法在对象本身找到需要的属性，就会继续访问对象的[[Prototype]] 链。

**构造函数**

可以使用 new 操作符和构造函数来创建一个新对象。

```javascript
function Employee(name) {
  this.name = name;
}
const employee = new Employee("Jane");
```

**继承**

JavaScript 通过将构造器函数与原型对象相关联的方式来实现继承。

```javascript
function Manager(name) {
  Employee.call(this, name);
  this.reports = [];
}
Manager.prototype = Object.create(Employee.prototype);
const manager = new Manager("Lucy");
```

**多态**

```javascript
Manager.prototype.work = function(hours) {
  Employee.prototype.work.call(this, hours);
}
```

### 对象关联风格的行为委托

```javascript
const Employee = {
  init: function(name) {
    this.name = name;
  },
  work: function() {
    // ...
  }
};
const Manager = Object.create(Employee);
Manager.reports = [];
Manager.init("Lucy");
```

### ES6 Class

只是现有原型机制的一种语法糖！！！

```javascript
class Employee {
  constructor(name) {
    this.name = name;
  }
  work() {
    console.log("Employee work");
  }
}
class Manager extends Employee {
  constructor(name) {
    super(name);
    this.reports = [];
  }
  
  work() {
    console.log("Manager work");
  }
}
const manager = new Manager("Lucy");
```

#### ES6 Class陷阱

避免在ES6 Class中修改原型链的属性和方法。

```javascript
class C {
  constructor() {
    C.prototype.count++;
    console.log( "Hello: " + this.count );
  }
}
C.prototype.count = 0;
var c1 = new C();
var c2 = new C();
```



