### 测试金字塔

![](/assets/test.png)

### STUB & MOCK

https://semaphoreci.com/community/tutorials/stubbing-and-mocking-with-mockito-2-and-junit

### 测试原则

* Fast
* Isolated/independent
* Repeatable
* Self-validating
* Thorough/Timely

### 单元测试

mockMvc

```java
@RunWith(SpringRunner.class)
@WebMvcTest(TaskController.class)
public class TaskControllerTest {
    @Autowired
    private MockMvc mockMvc;

    @MockBean
    private TaskService taskService;

    @Test
    public void should_get_all_tasks_by_getAllTask() throws Exception {
        given(taskService.getTasks()).willReturn(Lists.newArrayList(createTask("test"), createTask("aaa")));
        mockMvc.perform(MockMvcRequestBuilders.get("/tasks"))
                .andExpect(status().isOk())
                .andExpect(jsonPath("$[0].name").value("test"))
                .andExpect(jsonPath("$[1].name").value("aaa"));
    }

    public Task createTask(String name) {
        Task task = new Task();
        task.setName(name);
        return task;
    }
}
```

Mockito

```java
@RunWith(MockitoJUnitRunner.class)
public class TaskServiceTest {

    @InjectMocks
    private TaskService taskService;

    @Mock
    private TaskRepository taskRepository;

    @Test
    public void should_return_all_tasks_when_getAllTasks() {
        given(taskRepository.findAll()).willReturn(Lists.newArrayList(createTask("test"), createTask("aaa")));
        List<Task> tasks = taskService.getTasks();

        assertThat(tasks.size(), is(2));
        assertThat(tasks.get(0).getName(), is("test"));
        assertThat(tasks.get(1).getName(), is("aaa"));
    }

    public Task createTask(String name) {
        Task task = new Task();
        task.setName(name);
        return task;
    }
}
```

DataJpaTest

```java
@RunWith(SpringRunner.class)
@DataJpaTest
@AutoConfigureTestDatabase(replace = NONE)
public class TaskRepositoryTest {
    @Autowired
    private TaskRepository taskRepository;

    @Autowired
    private TestEntityManager entityManager;

    @Test
    public void get_all_will_return_all_tasks() {
        List<Task> tasks = taskRepository.findAll();
        assertThat(tasks.size(), is(2));
        assertThat(tasks.get(0).getName(), is("test"));
        assertThat(tasks.get(1).getName(), is("aaa"));
    }

}
```

### 集成测试 - TestRestTemplate

```java
@RunWith(SpringRunner.class)
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

### E2E测试

![](/assets/e2e.png)

### 契约测试

家里有个插座，买电器的时候需要考虑插头跟插座是能配对的，也就是说插座和插头之间需要有契约

![](/assets/contract.png)

因此，契约测试就是插座跟插头的配套性测试。

#### 怎么订契约

#### ![](/assets/cdct.png)

#### spring cloud contract

```java
import org.springframework.cloud.contract.spec.Contract

[
    Contract.make {
        name 'create clients by upload files'
        request {
            method "POST"
            url $(c("/auth/clients/import"), p("/clients/import"))
            headers {
                contentType('multipart/form-data;boundary=AaB03x')
            }
            multipart(
                file: named(
                    name: $(c(regex(nonEmpty())), p('clients.csv')),
                    content: $(c(regex(nonEmpty())), p('1234,小明\n' +    '1235,小红'))
                )
            )
        }
        response {
            status 200
        }
    }
]
```

实践

使用 spring cloud contract Tdd写Checked Todo List

