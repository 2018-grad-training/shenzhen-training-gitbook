## CSS基础介绍
CSS（层叠样式表）是用来样式化和排版你的网页的

### CSS是怎么工作的
Web浏览器将CSS规则应用于文档以影响它们的显示方式。它分两个阶段处理文档：
1. 浏览器将HTML和CSS转化成DOM（文档对象模型）。DOM在计算机内存中表示文档。它把文档内容和其样式结合在一起。
2. 浏览器显示 DOM 的内容。

![CSS工作机制](/images/css-rendering.jpg)

#### 浏览器工作原理
![浏览器工作原理](/images/browser-parsing-engine.jpg)

浏览器如何处理**image**？

浏览器如何处理**script**？
![浏览器处理脚本工作原理](/images/scripted-browser-parsing-engine.jpg)

#### CSS如何应用到HTML上？
HTML定义：
```html
<p>
  Let's use:
  <span>Cascading</span>
</p>
```
CSS定义：
```css
p {
  font-size: 14px;
}
span {
  color: blue;
  font-weight: bold;
}
```

- 外部样式表
- 内部样式表
- 内联样式

### 选择器
**例子**：如何选择该段落并为其添加背景色？[Jsbin](http://jsbin.com/kocaxenega/edit)
```html
<p class="paragraph" id="paragraph" data-name="paragraph">
  请将背景色设为黄色
</p>
```

- 简单选择器
    - `span`
    - `#id-name`
    - `.class-name`
- 属性选择器 `[data-quantity="3"]`
- 伪类 `:active`, `:nth-child(1)`
- 伪元素 `::after`, `::before`
- 组合器 
    - `.a, .b`
    - `.a .b`
    - `.a > .b`
    - `.a + .b`
    - `.a ~ .b`

### 层叠和继承
#### 层叠
1. 重要性 !important
2. 专用性
    
    - 元素选择器具有很低的专用性
    - 类选择器具有更高的专用性
    - ID选择器有甚至更高的专用性
3. 源代码次序

#### 继承
应用于某个元素的一些属性值将由该元素的子元素继承，而有些则不会。

### 盒模型

## CSS版面

### 浮动
#### 浮动是如何工作的?
浮动元素会脱离正常的文档布局流，并吸附到其父容器的左边。在正常布局中位于该浮动元素之下的内容，此时会围绕着浮动元素，填满其右侧的空间。

#### 清除浮动
```css
p {
    clear: both;
}
```

### 定位
- 静态定位
- 相对定位
- 绝对定位
- 固定定位

### Flexbox

## CSS延伸

### CSS最佳实践
- 使用合理的语义化命名
- 结构化／模块化
- 统一命名规范
- 遵循单一职责原则

### 浏览器兼容
- `-moz-` Firefox 
- `-webkit-` Safari and Chrome
- `-o-` Opera
- `-ms-` Internet Explorer

### CSS预处理语言
- Sass
- Less
- Stylus

```scss
$color-primary: #ff4466;

section .primary-button {
    background-color: $color-primary;
} 
```

---------

**CSS练习**

`git fetch origin css`