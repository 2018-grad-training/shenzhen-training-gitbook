#### TDD \(Test-driven Development\)

![](/assets/tdd.png)

#### 怎么写测试？

![](/assets/givenWhenThen.png)

#### 实践演示

##### 添加Junit5依赖

```
buildscript {
...
	dependencies {
		classpath('org.junit.platform:junit-platform-gradle-plugin:1.0.0')
	}
}

...

apply plugin: 'org.junit.platform.gradle.plugin'

...

dependencies {
...
    testCompile('org.junit.jupiter:junit-jupiter-api:5.0.0')
    testRuntime('org.junit.jupiter:junit-jupiter-engine:5.0.0')
}

```

```java
@ExtendWith(SpringExtension.class)
@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
public class DemoHelloWorldIntegrationTest {

    @Autowired
    private TestRestTemplate restTemplate;

    @Test
    public void guest_can_get_welcome_message() {
        ResponseEntity<String> response = restTemplate.getForEntity("/index", String.class);

        assertThat(response.getStatusCode(), is(HttpStatus.OK));
        assertThat(response.getBody(), is("welcome"));
    }

}
```

```

    @GetMapping("/index")
    private String welcome() {
        return "welcome";
    }

}
```



