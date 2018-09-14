## 异步数据流
**Stream**是一个不间断的按照时间顺序排列的event序列。它可以发出三样信号：值（value，对应于某些类型）、错误（error）和完成（completed）

![Click事件数据流](/images/rxjs-click-event-stream.png)

根据Stream发出的三种信号，那么我们就可以定义三个对应的执行函数异步的捕捉并处理这三种信号量。

```text
--a---b-c---d---X---|->
```

```text
Stream1:   ---c----c--c----c------c-->
           map(c becomes 1) 
           ---1----1--1----1------1-->
           scan(+)
Stream2:   ---1----2--3----4------5-->
```

## Rxjs入门

RxJS库通过使用 observable 序列来编写**异步**和**基于事件**的程序。

**Observable (可观察对象)**: 被观察的Stream，是一个可调用的未来值或事件的集合。

**Observer (观察者)**: 一个回调函数的集合，它知道如何去监听由 Observable 提供的值。

**Subscription (订阅)**: 表示 Observable 的执行／"监听"，主要用于取消 Observable 的执行。

**Operators (操作符)**: 使用像 map、filter、concat、flatMap 等这样的数组操作符，把异步事件作为集合来处理。

```typescript
var button = document.querySelector('button');
button.addEventListener('click', () => console.log('Clicked!'));
```

```typescript
var button = document.querySelector('button');
// Observable (可观察对象)
let observable = Rx.Observable.fromEvent(button, 'click');
// Observer (观察者)
let observer = {
  next: () => console.log('Clicked!')
}; 
// Subscription（订阅）
observable.subscribe(observer); 
```

### Observable
Observables 是多个值的惰性推送集合。

```javascript
var observable = Rx.Observable.create(function (x) {
  x.next(1);
  x.next(2);
  setTimeout(() => {
    x.next(4);
    x.complete();
  }, 1000);
});
```
当订阅下面代码中的 Observable 的时候会立即(同步地)推送值1、2，然后1秒后会推送值4，再然后是完成流。

#### Observable执行
- 创建 Observables
    
    Observables 可以使用 create 来创建, 但通常我们使用所谓的创建操作符, 像 of、from、interval、等等
- 订阅 Observables
```javascript
observable.subscribe(x => console.log(x));
```
- 执行 Observables
```javascript
 try {
    observer.next(1);
    observer.complete();
  } catch (err) {
    observer.error(err); // 如果捕获到异常会发送一个错误
  }
```
- 清理 Observables
```javascript
subscription.unsubscribe();
```

### Observer
观察者有三个回调函数的对象，每个回调函数对应一种 Observable 发送的通知类型。
```javascript
var observer = {
  next: x => console.log(x),
  error: err => console.error(err),
  complete: () => {},
};
```

### Subscription
Subscription 基本上只有一个 unsubscribe() 函数，这个函数用来释放资源或去取消 Observable 执行。

### Operators
操作符是 Observable 类型上的方法，比如 .map(...)、.filter(...)、.merge(...)，等等。
当操作符被调用时，它们不会改变已经存在的 Observable 实例。相反，它们返回一个新的 Observable ，它的 subscription 逻辑基于第一个 Observable 。

## Subject
是一种特殊类型的 Observable，它允许将值多播给多个观察者

## Rxjs处理请求
创建responseObservable
```typescript
const responseObservable = Rx.Observable.create((observer) => { 
    jQuery.getJSON("http://localhost:3000/users/") 
        .done((response) => observer.next(response)) 
        .fail((jqXHR, status, error) => observer.error(error)) 
        .always(() => observer.complete()) 
    });
```

订阅responseObservable
```typescript
responseObservable.subscribe(function(response){ 
    this.data = response;  
});
```