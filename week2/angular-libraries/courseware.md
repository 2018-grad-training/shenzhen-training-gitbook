## Angular库
- Angular库是开发人员为了解决一些同样的常见问题，而创建的一些通用解决方案，以便在不同的应用中重复使用。这些库可以作为 npm 包进行发布和共享。
- Angular库本身是不能运行的，必须在某个应用中导入库并使用它。

### 创建库
使用 Angular CLI，用以下命令在新的工作空间中生成一个新库的骨架：
```typescript
ng new my-workspace --create-application=false
cd my-workspace
ng generate library <my-lib> --prefix <my-prefix>
```
生成一个新库时， angular.json 中也增加了一个 'library' 类型的项目：
```json
"projects": {
  ...
  "my-lib": {
    "root": "projects/my-lib",
    "sourceRoot": "projects/my-lib/src",
    "projectType": "library",
    "prefix": "lib",
    "architect": {
      "build": {
        "builder": "@angular-devkit/build-ng-packagr:build",
        ...
```

### 开发库

##### - 库文件夹下的 public-api.ts 文件中维护库的公共 API (需要导出的功能)，库被导入应用时，从此文件导出的所有内容都会公开。
```typescript
export * from './lib/service/my-service.service';
export * from './lib/component/my-component.component';
```

##### - 库文件夹下的 ng-package.json 是专门针对 ng-packagr 的一个打包配置文件。
- 可在 $schema 对应路径下，查找可配置的内容。
- whitelistedNonPeerDependencies: ng-packagr 默认会根据 package.json 的 peerDependencies 节点清单来决定库所需要的第三方依赖包，这些依赖包不会被打包至库。
然而，所依赖包不存在 peerDependencies 节点里时，就需要配置此属性。
- lib/entryFile：指定入口文件。
```json
{
  "$schema": "../../node_modules/ng-packagr/ng-package.schema.json",
  "dest": "../../dist/my-lib",
  "lib": {
    "entryFile": "src/public_api.ts"
  },
  ...
}
```

##### - 库文件夹下的 tsconfig.json 文件决定了打包库的时候，ts文件将是以什么样的形式生成。
```json
{
  ...
  "include": [
    "./**/*.ts",
    "./**/*.d.ts"
  ],
  "exclude": [
    "src/test.ts",
    "**/*.spec.ts"
  ],
  ...
}
```

##### - 使用 CLI 命令来构建、测试和 lint 这个项目：
```typescript
ng build my-lib
ng test my-lib
ng lint my-lib
```

### 发布库
将库发布到 NPM (需创建用户账号)。
```typescript
ng build my-lib --prod
cd dist/my-lib
npm publish
```

### 在应用中使用自己的库
不需把库发布到 npm 包管理器上，就可以在自己的应用中使用它。
##### 1. 构建库
```typescript
ng build my-lib
```
##### 2. 在应用中，按名字从库中导入
```typescript
import { myExport } from 'my-lib';
```

#### 练习：
###### 1. 创建库，包含自定义组件和自定义服务
###### 2. 在应用中使用新创建库中的组件和服务
