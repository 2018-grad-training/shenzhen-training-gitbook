### Spring Data JPA介绍

```java
@Table(name = "companies")
@Entity
public class Company {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "id")
    private Long id;

    @Column(name = "code")
    private String code;

    @Column(name = "name")
    private String name;
}
```

### JpaRepository

[https://docs.spring.io/spring-data/jpa/docs/1.9.1.RELEASE/reference/html/\#jpa.query-methods.query-creation](https://docs.spring.io/spring-data/jpa/docs/1.9.1.RELEASE/reference/html/#jpa.query-methods.query-creation)![](/assets/jpa_keyword.png)[https://docs.spring.io/spring-data/jpa/docs/1.9.1.RELEASE/reference/html/\#jpa.query-methods.query-creation](https://docs.spring.io/spring-data/jpa/docs/1.9.1.RELEASE/reference/html/#jpa.query-methods.query-creation)

### 练习

#### 引入Spring Data JPA

```
compile('org.springframework.boot:spring-boot-starter-data-jpa')
compile('mysql:mysql-connector-java:6.0.6')
```

#### 配置mysql

```
spring.datasource.url=jdbc:mysql://localhost:3307/demo
spring.datasource.username=root
spring.datasource.password=abc123
```

#### 使用docker启动mysql

```bash
docker pull mysql:5.6.23
docker run -d -p 3307:3306 --name hule-mysql -e MYSQL_ROOT_PASSWORD=abc123 -e MYSQL_DATABASE=demo mysql:5.6.23
```

#### TDD的方式 创建／删除／查看Task



