### Gradle作用

gradle自动化构建工具

### 创建Gradle项目

```bash
$ gradle init --type java-application

apply plugin: ‘idea’
```

```
├── build.gradle
├── gradle    
│   └── wrapper
│       ├── gradle-wrapper.jar
│       └── gradle-wrapper.properties
├── gradlew
├── gradlew.bat
├── settings.gradle
└── src
    ├── main
    │   └── java  
    │       └── App.java
    └── test      
        └── java
            └── AppTest.java
```

```
./gradlew run

./gradlew test
```

### build.gradle详解

```
apply plugin: 'java'
apply plugin: 'application'

repositories {
    jcenter()
}

dependencies {
    compile 'com.google.guava:guava:22.0'
    testCompile 'junit:junit:4.12'
}

mainClassName = 'App'
```



