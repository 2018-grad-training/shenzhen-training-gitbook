### 测试金字塔

![](/assets/test.png)

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

![](/assets/contract-test.png)

#### moco & moscow

[https://github.com/macdao/moscow](https://github.com/macdao/moscow)

[https://github.com/dreamhead/moco](https://github.com/dreamhead/moco)

```js
[
  {
    "request": {
      "method": "POST",
      "uri": "/auth/token.action",
      "headers": {
        "Content-Type": "application/x-www-form-urlencoded"
      },
      "queries": {
        "grant_type": "client_credentials",
        "client_id": "549ee506fcd669c6eb2de075e3008d4d",
        "client_secret": "e8898b30e92b2e60f491ca3447494db1"
      }
    },
    "response": {
      "status": 200,
      "json": {
        "token_type": "mac",
        "expires_in": 7200,
        "refresh_token": "175b3da4854e33a45497f3f2b3e4",
        "access_token": "84d287257fbecd4be233dc74c96ade5"
      }
    }
  }
]
```

#### spring cloud contract



