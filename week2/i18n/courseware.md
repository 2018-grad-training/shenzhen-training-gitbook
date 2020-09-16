## Angular国际化（i18n）与本地化
### 国际化：用于对应用进行设计和准备，以便在全球不同地区使用。
- 使用内置管道，将日期、数字、百分比和货币显示成本地格式。
- 标记出模板中要翻译的文字。
- 标记出要翻译的表达式的复数形式。
- 标记出要翻译的备用文字。

### 本地化：为不同的本地环境构建应用版本。
- 把标记过的文本提取到源语言文件中。
- 把这个文件为每种语言复制一份，提供给翻译人员或翻译服务。
- 为本地环境构建应用时，合并这些翻译完成的文件。


### 应用本地化的步骤
#### 1. 添加 localize 包
```typescript
ng add @angular/localize
```

#### 2. 按 ID 引用本地环境
使用 Unicode 本地环境标识符（ID）引用本地环境，指定语言、国家/地区以及其他变体或细分的可选代码。

该 ID 由一个语言标识符，短划线（-）和本地环境扩展组成。比如，en-US 是指美国英语区，fr-CA 是指加拿大法语区。Angular 默认使用 en-US（美国英语）作为应用的源本地环境。

#### 3. 根据本地环境格式化数据
Angular内置的管道 ，根据本地化的规则使用 LOCALE_ID 令牌格式化数据：

- DatePipe：格式化日期值。
- CurrencyPipe：把数字转换成货币字符串。
- DecimalPipe：把数字转换成十进制数的字符串。
- PercentPipe：把数字转换成百分比字符串。

例如：
```typescript
{{amount | currency : 'en-US'}}
```

#### 4. 准备翻译模板
（1）用 i18n 属性标记要翻译的文本
```html
<h1 i18n>Hello i18n!</h1>
```

（2）添加有用的描述和含义到 i18n 属性的值中
```html
<h1 i18n="site header|An introduction header for this sample">Hello i18n!</h1>
```

（3）翻译不显示的文字
```html
<ng-container i18n>I don't output any element</ng-container>
```

（4）标记要翻译的元素属性（i18n-属性名）
```html
<img [src]="logo" i18n-title title="Angular logo" />
```

（5）标记复数形式和替换形式
```html
<span i18n>Updated {minutes, plural, =0 {just now} =1 {one minute ago} other {{{minutes}} minutes ago}}</span>
```

#### 5. 使用翻译文件
（1）提取源语言文件：使用 Angular CLI 的 xi18n 命令，把模板中标记过的文本（i18n，i18n-属性名）提取到源语言文件中
```typescript
ng xi18n
```

（2）为每种语言创建一个翻译文件，例如：
```typescript
法语翻译文件：messages.fr.xlf
西班牙语翻译文件：messages.es.xlf
```

（3）翻译每个翻译文件 

（4）单独翻译复数形式和替代表达式 

#### 6. 把翻译合并到应用中
（1）在angular.json中定义本地环境
- sourceLocale：应用源代码中使用的本地环境（默认为 en-US ）
- locales：本地环境标识符到翻译文件的映射表
```json
...
"projects": {
  "angular.io-example": {
    ...
    "i18n": {
      "sourceLocale": "en-US",
      "locales": {
        "fr": "src/locale/messages.fr.xlf"
      }
    }
  }
}
```

（2）为每种本地环境生成一个应用版本(angular.json 的"localize" 选项)
- 把 "localize" 设置为 true，构建所有本地环境版本。
```json
...
"build": {
  "options": {
    "localize": true,
    ...
```

- 把 "localize" 设置为本地环境标识符子集，只构建部分本地环境版本。
```json
...
"build": {
  "options": {
    "localize": ["fr"],
    ...
```

#### 7. 部署多个本地环境
