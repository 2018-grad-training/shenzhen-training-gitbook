#### TDD \(Test-driven Development\)

![](/assets/tdd.png)

#### 怎么写测试？

![](/assets/givenWhenThen.png)

#### 实践演示

##### Hello world！

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
        assertThat(response.getBody(), is("Hello world"));
    }

}
```

```java
{
    @GetMapping("/index")
    private String welcome() {
        return "Hello world";
    }

}
```



