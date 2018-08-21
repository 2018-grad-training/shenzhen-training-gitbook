# Dependency Injection

### 注入方式

* 基于构造函数\(recommended\)

```java
public class SimpleMovieLister {
    private MovieFinder movieFinder;

    public SimpleMovieLister(MovieFinder movieFinder) {
        this.movieFinder = movieFinder;
    }
}
```

* 基于setter方法

```java
public class SimpleMovieLister {

    private MovieFinder movieFinder;

    public void setMovieFinder(MovieFinder movieFinder) {
        this.movieFinder = movieFinder;
    }
}
```



