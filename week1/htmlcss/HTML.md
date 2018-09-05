## HTML定义
HTML（超文本标记语言——HyperText Markup Language）

**HTML & CSS & Javascript关系**

**HTML**：网页的内容和基本布局

**CSS**：网页的表现与展示效果

**Javascript**：网页的功能与行为

## HTML是怎么工作的
![HTML工作机制](/images/html-parsing.jpg)

```html
<html>
    <head></head>
    <body>
        <p>
          Let's use: Cascading
        </p>    
    </body>
</html>
```
DOM树:
```text
#document
└─ HTML
    ├─ HEAD
    └─ BODY
         └─ P
            └─ "Let's use: Cascading"
```

## 在线编辑工具
- [JSBin](http://jsbin.com/?html,js,output)
- [Thimble](https://thimble.mozilla.org/zh-CN/)

## HTML基础介绍
### HTML元素
![HTML 元素](/images/html-element.png)

#### 嵌套元素

#### 空元素

#### 块级元素和内联元素
**块级元素**：在页面中以块的形式展现 —— 相对与其前面的内容它会出现在新的一行，其后的内容也会被挤到下一行展现

**内联元素**：通常出现在块级元素中并包裹文档内容的一小部分

- 一个以block形式展现的块级元素不会被嵌套进内联元素中，但可以嵌套在其它块级元素中。
- 默认情况下，块级元素的内容宽度是其父元素的宽度的100％，并且与其内容一样高。
- 内联元素高宽与他们的内容高宽一样。您不能对内联元素设置宽度或高度——它们只是位于块级元素的内容中。

**默认浏览器有默认的展示不同元素的CSS样式**

#### 空元素
只有一个标签，通常用来在此元素所在位置插入/嵌入一些东西

## HTML文档
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <meta name="author" content="Du Juan">
    <meta name="description" content="...">
    <title>My test page</title>
    <link rel="stylesheet" href="style.css">
  </head>
  <body>
    <p>This is my page</p>
    <script src="index.js"></script>
  </body>
</html>
``` 

`meta`: 元数据。指定包含关于页面内容的关键字，可能会让你的页面在搜索引擎的相关的搜索出现得更多(SEO)。

**练习**：创建一个空页面，包含html文档和css，js文件的引用

### HTML语义

https://developer.mozilla.org/zh-CN/docs/Learn/HTML/Introduction_to_HTML/HTML_text_fundamentals

#### 语义化标签的优点：
- 比`<div>`标签有更加丰富的含义，方便开发与维护
- 搜索引擎能更方便的识别页面的每个部分
- 方便其他设备解析（如移动设备、盲人阅读器等）

#### HTML5
 
##### 新的HTML5元素
- 新的语义元素： `<header>` `<footer>` `<article>` `<section>` 等
- 新Form元素属性：number, date, time, calendar, and range
- 新的图形元素：`<svg>` 和 `<canvas>`
- 新的多媒体元素：`<audio>`和 `<video>`

##### 新的HTML5 API
- HTML地理位置
- HTML拖放
- HTML Local Storage
- HTML应用程序缓存

-------

[HTML练习](https://github.com/2018-grad-training/tw-resume-htmlcss-base)