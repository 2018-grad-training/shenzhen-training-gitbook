## Angular测试需要的工具

- 测试运行器：**Karma**
- 前端测试框架：**Jasmine**
- Angular测试工具：**Testbed**
- 端到端测试：**Protractor**

### 测试配置
CLI 会生成Jasmine和Karma的配置文件。也可以通过编辑karma.conf.js和test.ts文件来修改配置。

### Angular Testbed（测试机床）
Angular为单元测试提供了Testbed。 TestBed 会动态创建一个用来模拟 @NgModule 的 Angular 测试模块来提供一个测试上下文环境。

```typescript
describe('TestComponent', () => {
  beforeEach(async(() => {
    // Testbed异步创建Angular测试模块
  }));
  beforeEach(() => {
    // Testbed创建并准备测试组件
  });
  it('should ...', () => {
    // 测试组件行为是否符合期望
  });
});
```

## Angular测试

### 组件测试
#### 准备测试模块
```typescript
  beforeEach(async(() => {
    TestBed.configureTestingModule({
      declarations: [ TestComponent ]
    })
    .compileComponents();
  }));
```
#### 创建测试组件
```typescript
  let component: TestComponent;
  let fixture: ComponentFixture<TestComponent>;
  
  beforeEach(() => {
    fixture = TestBed.createComponent(TestComponent);
    component = fixture.componentInstance;
    fixture.detectChanges();
  });
```
- ComponentFixture 是一个测试挽具，用来与所创建的组件及其DOM元素进行交互。
- 可以通过测试夹具（fixture）来访问该组件的实例。
- 测试程序必须手动调用 fixture.detectChange()，来触发新一轮的变更检测周期。

#### 组件DOM测试
```typescript
  it('should value change when click button', () => {
    const demoElement: HTMLElement = fixture.nativeElement;
    const p = demoElement.querySelector('p');
    const button = demoElement.querySelector('button');

    button.click();
    fixture.detectChanges();

    expect(p.textContent).toBe('new value');
  });
```
练习：[组件测试demo](https://github.com/2018-grad-training/tw-angular-test)

#### 组件JS测试 
```typescript
  it('should value change when onClick be called', () => {
    component.onClick();
    expect(component.value).toBe('new value');
  });
```

练习：[组件测试demo](https://github.com/2018-grad-training/tw-angular-test)

#### Stub组件依赖
![Stub组件依赖](/images/angular-test-service-stub.jpg)

##### 提供服务的测试替身
```typescript
const userServiceStub = {
  isLoggedIn: () => true,
  userName: 'fake-name'
};
```
##### 添加Service依赖
```typescript
TestBed.configureTestingModule({
  declarations: [ StubComponent ],
  providers: [ {provide: UserService, useValue: userServiceStub } ]
})
```
##### 获取注入的服务
```typescript
userService = fixture.debugElement.injector.get(UserService);
```
练习：[组件测试stub](https://github.com/2018-grad-training/tw-angular-test)

#### 测试组件异步服务
当测试组件时，只应该关心服务的公共 API。 通常来说，测试不应该自己向远端服务器发起调用。 它们应该对这些调用进行仿真。

##### 使用间谍（Spy）进行测试
```typescript
const todoService = jasmine.createSpyObj('TodoService', ['getList']);
getTodoListSpy = todoService.getList.and.returnValue( of(todoListArray) );
```
题目: 给todo ListComponent添加测试

#### 测试嵌套组件

##### 对不需要的组件提供桩（stub）
```typescript
@Component({selector: 'app-child', template: ''})
class ChildStubComponent {}
```
题目: 添加ParentComponent和ChildComponent，对ChildComponent进行mock

### 服务测试
练习：[服务测试service](https://github.com/2018-grad-training/tw-angular-test)

题目：添加todo TodoService测试

### 属性指令测试

练习：给HighlightDirective添加测试

### 管道测试

练习：给Pipe添加测试