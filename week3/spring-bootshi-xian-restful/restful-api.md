### REST

Representational State Transfer，表述性状态转移。REST是一组架构约束条件和原则。

### **REST成熟度模型**

#### **第0级：使用HTTP作为传输方式；一个URI，一个HTTP方法**

```bash
POST /InStock HTTP/1.1
Host: www.example.org
Content-Type: application/soap+xml; charset=utf-8
Content-Length: nnn

<?xml version="1.0"?>
<soap:Envelope
xmlns:soap="http://www.w3.org/2001/12/soap-envelope"
soap:encodingStyle="http://www.w3.org/2001/12/soap-encoding">

<soap:Body xmlns:m="http://www.example.org/stock">
  <m:GetStockPrice>
    <m:StockName>IBM</m:StockName>
  </m:GetStockPrice>
</soap:Body>

</soap:Envelope>
```

```bash
HTTP/1.1 200 OK
Content-Type: application/soap+xml; charset=utf-8
Content-Length: nnn

<?xml version="1.0"?>
<soap:Envelope
xmlns:soap="http://www.w3.org/2001/12/soap-envelope"
soap:encodingStyle="http://www.w3.org/2001/12/soap-encoding">

<soap:Body xmlns:m="http://www.example.org/stock">
  <m:GetStockPriceResponse>
    <m:Price>34.5</m:Price>
  </m:GetStockPriceResponse>
</soap:Body>

</soap:Envelope>
```

#### **第1级：引入了资源的概念，每个资源有对应的标识符和表达；多个URI，一个HTTP方法**

```
GET http://example.com/app/createUser
GET http://example.com/app/getUser?id=123
GET http://example.com/app/changeUser?id=123&field=value
GET http://example.com/app/deleteUser?id=123
```

#### **第2级：根据语义使用HTTP动词，适当处理HTTP响应状态码；多个URI，多个HTTP方法**

##### HTTP方法

POST（CREATE）：在服务器新建一个资源。

GET（READ）：从服务器取出资源（一项或多项）。

PUT（UPDATE）：在服务器更新资源。

DELETE（DELETE）：从服务器删除资源。

```
POST http://example.com/app/users
{ 
    "name" : "Alice"
}

GET http://example.com/app/users/123
{ 
    "id" : "123"
    "name" : "Alice"
}

PUT http://example.com/app/users/123
{ 
    "id" : "123"
    "name" : "Alice1"
}

DELETE http://example.com/app/users/123
```

##### 常用状态码

| HTTP code | Message | Description |
| :--- | :--- | :--- |
| 200 | OK | 成功 |
| 201 | Created | 创建成功 |
| 204 | No Content | 成功且没有返回内容 |
| 400 | Bad Request | 请求URL存在，但是request有问题，比如缺少参数，参数不合法，参数错误 |
| 401 | Unauthorized | 用户认证失败 |
| 403 | Forbidden | 没有权限查看／操作 |
| 404 | Not Found | 没有找到 |
| 500 | Server Error | 服务器端错误 |

#### **第3级：使用超媒体作为应用状态引擎（HATEOAS）；多个URI，多个HTTP方法**

```
GET http://example.com/app/users
{
    "content": [ {
        "name": "Alice",
        "links": [ {
            "rel": "self",
            "href": "http://example.com/app/users/1"
            }, {
            "rel": "allOrders"
            "href": "http://example.com/app/users/1/orders"
        } ]
    },{
        "name": "Bob",
        "links": [ {
            "rel": "self",
            "href": "http://example.com/app/users/2"
        },{
            "rel": "allOrders"
            "href": "http://example.com/app/users/2/orders"
        } ]    
    }],
    "links": [ {
        "rel": "self",
        "href": "http://example.com/app/users"
    } ]
}
```

### 优势

* URL具有很强可读性的，具有自描述性；
* 资源描述与视图的松耦合；
* 可提供OpenAPI，便于第三方系统集成，提高互操作性；
* 提供无状态的服务接口，可提高应用的水平扩展性；

### 练习

在spring boot项目上添加三个RESTFul API

* 查看所有task集合
* 添加task
* 删除task



