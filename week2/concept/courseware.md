## 前端框架的演进

## Angular应用的架构

### 单页面应用的构成
- 功能模块
- 路由／前端视图
- 组件
- 服务

### Angular应用的架构
![Angular应用架构](/images/angular-architechure.jpg)

**模块**：用来将应用中不同部分组织成一个Angular框架可以理解的单元

**组件**：是Angular应用的基本构建块，可以把一个组件理解为一段带有业务逻辑和数据的HTML。

**服务**：用来封装可重用的业务逻辑。

## Angular命令行工具
```
npm install -g @angular/cli
```

创建一个新工程：`ng new [project-name]`

启动工程: `ng serve`

运行测试: `ng test`

构建工程: `ng build`

生成Angular元素：`ng generate component [name]`

## Angular核心概念

### 模块NgModule
Angular 的基本构造块是 NgModule，它为组件提供了**编译的上下文环境**。NgModule 会把相关的代码收集到一些功能集中。
Angular 应用就是由一组 NgModule 定义出的。 应用至少会有一个用于引导应用的根模块，通常还会有很多特性模块。

#### 根模块
根模块就是你用来启动此应用的模块。
```typescript
@NgModule({
  declarations: [AppComponent],
  imports: [BrowserModule],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

- declarations —— 告诉 Angular 哪些组件属于该模块。
- imports —— 导入 BrowserModule 使应用能够在浏览器渲染。
- providers —— 各种服务提供商。
- bootstrap —— 根组件，Angular 创建它并插入 index.html 宿主页面。

#### 特性模块
根模块可以包含任意深度的层次化子模块（特性模块）。

创建一个特性模块： `ng generate module todo`

#### Angular自定义模块
```typescript
import { BrowserModule } from '@angular/platform-browser';
@NgModule({
  imports: [ BrowserModule ],
  ...
});
```

### 组件Component
每个组件都会定义一个类，其中包含应用的数据和逻辑，并与一个 HTML 模板相关联，该模板定义了一个供目标环境下显示的视图。

创建一个组件： `ng generate component list`

#### NgModule和组件
NgModule 为其中的组件提供了一个编译上下文环境。模块总会有一个根组件，并在启动时创建它。

模块可以包含任意数量的其它组件，这些组件可以通过路由器加载，也可以通过模板创建。那些属于这个 NgModule 的组件会共享同一个编译上下文环境。

#### 模板语法
##### 数据绑定
![数据绑定](/images/angular-data-binding.png)

- 插值表达式 `{ {title} }`
- 属性绑定 `[value]="property"`
- 事件绑定 `(click)="onClicked($event)"`
- 双向数据绑定 `[(ngModel)]="inputValue"`

![双向绑定](/images/angular-component-databinding.png)

##### 指令
- 结构型指令 `*ngFor`, `*ngIf` ...
- 属性型指令 `ngClass`, `ngStyle` ...

练习：https://github.com/2018-grad-training/tw-basic-angular /template-syntax

#### 生命周期钩子
组件的实例有一个生命周期：**新建**、**更新**和**销毁**。

练习：https://github.com/2018-grad-training/tw-basic-angular /lifecycle

题目：新建父组件Parent，和自组件ChildA，ChildB。Parent中属性sharedValue作为ChildA，ChildB共同的Input，Parent中属性valueA作为ChildA
的输入。查看更新和销毁ChildA，ChildB时的生命周期Log。

#### 组件交互
- 父组件传递数据到子组件
- 父组件监听子组件的事件
- 父组件与子组件通过本地变量互动 

    `<app-child #child></app-child>`
- 父组件调用
    
    `@ViewChild(ChildComponent) private childComponent: ChildComponent;`
- 父组件和子组件通过服务来通讯

练习：https://github.com/2018-grad-training/tw-basic-angular /component-interaction

题目1：通过本地变量实现父组件与子组件的通信

题目2：通过父组件调用实现父组件与子组件的通信

题目3：通过服务实现父组件与子组件的通信

### 指令Directive

在 Angular 中有三种类型的指令：
- 组件 — 拥有模板的指令
- 属性型指令 — 改变元素、组件或其它指令的外观和行为的指令
- 结构型指令 — 通过添加和移除 DOM 元素改变 DOM 布局的指令

创建一个指令：`ng generate directive highlight`

### 服务Service
组件是服务的消费者，也就是说，你可以把一个服务注入到组件中，让组件类得以访问该服务类。

创建一个服务：`ng generate service alert`

#### 依赖注入
Angular 会在启动过程中为你创建全应用级**注入器**。在应用中要用到的任何类都必须使用该应用的注入器注册一个**提供商**，以便注入器可以使用它来创建新实例。
当创建组件类的新实例后，我们就可以通过该组件类的**构造函数**来访问该服务。

![依赖注入](/images/angular-injector-injects.png)

1. 通过注入器注册一个服务
```typescript
@Injectable()
export class LoggerService {}
```
2. 通过提供商提供服务
```typescript
@Component({
  providers:  [ LoggerService ]
})
```
3. 通过构造函数访问该服务
```typescript
constructor (private logger: LoggerService) {}
```

题目：创建一个全局可用／NgModule可用／组件可用 的服务，可以alert信息。

### 管道Pipe
管道把数据作为输入，然后转换它，给出期望的输出

- 内置管道
- 自定义管道