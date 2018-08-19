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
    
只有对象！！！

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
    // ...
  }
}
class Manager extends Employee {
  constructor(name) {
    super(name);
    this.reports = [];
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
```