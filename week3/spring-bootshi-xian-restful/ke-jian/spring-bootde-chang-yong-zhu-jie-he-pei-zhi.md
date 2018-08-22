#### TDD \(Test-driven Development\)

![](/assets/tdd.png)

#### 怎么写测试？

![](/assets/givenWhenThen.png)

#### 实践演示

```java
@RunWith(SpringRunner.class)
@SpringBootTest
public class DemoHelloWorldTest {
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
@RestController
public class DemoHelloWorldController {

    @GetMapping("/index")
    private String welcome() {
        return "welcome";
    }

}
```



