## Angular风格指南
参考[Angular风格指南](https://angular.cn/guide/styleguide)

- 单一职责
- 命名
- 编程约定
- 层次化注入服务

## 应用程序结构
```
├── product
│   ├── shared
│   |   ├── directive
│   |   └── pipe
│   ├── product-detail
│   └── product-list
│       └── product-item
├── question
│   ├── shared
│   |   └── question-item
│   ├── question-detail
│   └── question-list
├── core
│   ├── interceptors
│   ├── not-found
│   └── services
├── shared
│   ├── bread-crumbs
│   └── search-bar
```
- 根模块
- 特性模块
- 共享特性模块
    - 不要在共享模块中提供服务。服务通常是单例的，应该在整个应用或一个特定的特性模块中只有一份。
    - 在 SharedModule 中导入所有模块都需要的资产（例如 CommonModule 和 FormsModule）
- 核心特性模块
    - 考虑把那些数量庞大、辅助性的、只用一次的类收集到核心模块中，让特性模块的结构更清晰简明。
    - CoreModule 提供了一个或多个单例服务。Angular 使用应用的根注入器注册这些服务提供商，让每个服务的这个单例对象对所有需要它们的组件都是可用的
    - 避免在 AppModule 之外的任何地方导入 CoreModule。
    