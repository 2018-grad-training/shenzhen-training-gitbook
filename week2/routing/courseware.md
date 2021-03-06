## Angular路由
Angular 的路由器能让用户从一个视图导航到另一个视图。Angular路由是显示应用内部的URL路径，它和服务器端路由不同，只是看起来一致罢了。
```html
<base href="/">
```
浏览器会用 `<base href>` 的值作为相对URL 的前缀，当前引用的CSS 文件、脚本和图片也是基于这个相对URL。

## 路由注册
### 配置路由
```typescript
const appRoutes: Routes = [
  { path: 'index', component: IndexComponent },
  { path: '',
    redirectTo: '/index',
    pathMatch: 'full'
  },
  { path: '**', component: PageNotFoundComponent }
];

@NgModule({
  imports: [
    RouterModule.forRoot(appRoutes)
  ],
})
export class AppModule { }
```

路由器使用先匹配者优先的策略来选择路由。

### 路由模块

### 绑定试图
```html
<router-outlet></router-outlet>
```

## 路由访问
### 路由器链接
```html
<a routerLink="/index" routerLinkActive="active">首页</a>
```
### 组件内访问
```typescript
constructor( private router: Router) { }
linkToIndex() {
  this.router.navigate(['/index']);
}
```

## 特性模块路由
- 根模块 AppRoutingModule 中，调用 RouterModule.forRoot注册应用的顶级路由
- 在特性模块中，调用RouterModule.forChild方法来注册附属路由。
```typescript
const routes: Routes = [{
    path: 'index',
    component: IndexComponent
}];
@NgModule({
    imports: [ RouterModule.forChild(routes)],
    exports: [ RouterModule ]
})
export class FeatureRoutingModule { }
```
```typescript
@NgModule({
  imports: [
    FeatureRoutingModule
  ]
})
export class FeatureModule {}
```

## 惰性加载
通过引进异步路由，可以获得在请求时才惰性加载特性模块的能力。 

### 为什么需要惰性加载？
- 只在用户请求时才加载某些特性区。
- 对于那些只访问应用程序某些区域的用户，这样能加快加载速度。
- 你可以持续扩充惰性加载特性区的功能，而不用增加初始加载的包体积。

### 配置路由
```typescript
{
  path: 'admin',
  loadChildren: () => import('app/admin/admin.module').then(m => m.AdminModule)
}
```

## 预加载
预加载是介于立即加载和惰性加载的一种方式。应用启动时进行立即加载，然后几乎立即开始后台加载配置了预加载的模块。
