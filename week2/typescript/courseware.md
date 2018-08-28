TypeScript是JavaScript语言的超集，Typescript支持最新的JavaScript语言特性之外，还增加了非常有用的**编译时类型检查**特性，
而代码又最终会编译成 JavaScript 来执行。

Javascript：
```javascript
function add(a, b) {
  return a + b;
}
add(1, '3');
```
Typescript：
```typescript
function add(a: number, b: number) {
  return a + b;
}
add(1, '3');
```
TypeScript的类型检查是在编译期进行的，编译后的 JavaScript 代码并不会增加任何类型检查相关的代码。

## Typescript编译器
安装：`npm install -g typescript`

编译：`tsc helloworld.ts`

https://github.com/2018-grad-training/tw-js-scaffold

## Typescript常见类型
### 基础类型
- boolean
- number
- string
- 数组 `let list: number[] = [1,2,3]`
- enum 
```typescript
  enum Color { Red, Green, Blue }; 
  let c: Color = Color.Green
```
- any
- void
- null / undefined

### 接口interface
```typescript
interface Point {
  color: string;
  width?: number;
  readonly position: number;
}
let p: Point = {color: 'white', position: 1};
```

### 类class
```typescript
class Person {
  protected name: string;
  constructor(name: string) {
    this.name = name;
  }
}

class Employee extends Person {
  private department: string;

  constructor(name: string, department: string) {
    super(name);
    this.department = department;
  }

  public getElevatorPitch() {
    return `Hello, my name is ${this.name} and I work in ${this.department}.`;
  }
}
```

- Typescript增加了public, private, protected, readonly等访问控制修饰符
- Typescript实现了抽象类

### 函数function
```typescript
function add(x: number, y: number): number {
    return x + y;
}
```
**可选参数**
```typescript
function buildName(firstName: string, lastName?: string) {
}
```
**默认参数**
```typescript
function buildName(firstName: string, lastName = "Smith") {
}
```
**剩余参数**
```typescript
function buildName(firstName: string, ...restOfName: string[]) {
  return firstName + " " + restOfName.join(" ");
}
let employeeName = buildName("Joseph", "Samuel", "Lucas", "MacKinzie");
```


## 类型断言
类型断言好比其它语言里的类型转换，但是不进行特殊的数据检查和解构。

```typescript
let strLength: number = (<string>someValue).length;
```

```typescript
let strLength: number = (someValue as string).length;
```


