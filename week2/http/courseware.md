HttpClient 是 Angular 通过 HTTP 与远程服务器通讯的机制。它基于浏览器提供的 XMLHttpRequest 接口。

## 获取数据
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

## 发送数据到服务器
Service中发起POST请求
```typescript
addTodo (todo: Todo): Observable<Todo> {
    return this.http.post<Todo>(this.todoUrl, todo, httpOptions);
}
```

### 请求头
```typescript
import { HttpHeaders } from '@angular/common/http';

const httpOptions = {
  headers: new HttpHeaders({
    'Content-Type':  'application/json',
    'Authorization': 'my-auth-token'
  })
};
```
