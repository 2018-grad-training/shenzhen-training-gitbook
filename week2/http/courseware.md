## 异步请求模型
### 回调

把函数作为参数传入到另一个函数中。这个函数就是所谓的回调函数。JavaScript 的回调是在异步调用场景下使用的。

```javascript
var func1 = function(callback){
  setTimeout(function() {
    callback();
  }, 1000);
}
```
### Promise

Promise解决了回调黑洞问题。它简单说就是一个容器，里面保存着异步操作的结果。  

```javascript
const promise = new Promise(function(resolve, reject) {
  if (/* 异步操作成功 */){
    resolve(value);
  } else {
    reject(error);
  }
});

promise.then(function() {
  // ... 
});
```
常见的实现有jQuery的$.ajax(), ES6的Promise，Fetch API

### 发布／订阅
发布/订阅模式可以广泛用于异步编程中，代替传递回掉函数的方案，比如，我们可以订阅 ajax 请求的 error、success 等事件。发布者和订阅者之间解耦。

## HttpClient
HttpClient 是 Angular 通过 HTTP 与远程服务器通讯的机制。它基于浏览器提供的 XMLHttpRequest 接口。

### 获取数据
1. 导入模块
```typescript
imports: [
    BrowserModule,
    HttpClientModule,
]
```
2. 注入HttpClient
```typescript
@Injectable()
export class TodoService {
    constructor(private http: HttpClient) { }
}
```
3. Service中发起请求
```typescript
getList() {
    return this.http.get<Todo[]>(this.todoUrl);
}
```
4. 组件中处理请求
```typescript
getTodoList() {
    this.todoService.getList()
        .subscribe(
          (data: Todo[]) => this.todoList = data,
          (error) => console.log(error)
        );
}
```

### 发送数据到服务器
Service中发起POST请求
```typescript
addTodo (todo: Todo): Observable<Todo> {
    return this.http.post<Todo>(this.todoUrl, todo, httpOptions);
}
```

#### 请求头
```typescript
import { HttpHeaders } from '@angular/common/http';

const httpOptions = {
  headers: new HttpHeaders({
    'Content-Type':  'application/json',
    'Authorization': 'my-auth-token'
  })
};
```
