---
title: "CSS选择器详解"
slug: "css-selectors"
sequence: 4
description: "深入理解CSS选择器的类型、优先级和使用技巧"
is_published: true
estimated_minutes: 40
language: "zh-CN"
---

# CSS 选择器详解

## 基础选择器

### 1. 通用选择器

选择所有元素：

```css
* {
    margin: 0;
    padding: 0;
}
```

### 2. 元素选择器

根据标签名选择元素：

```css
p {
    color: blue;
}

h1 {
    font-size: 24px;
}
```

### 3. 类选择器

使用 `.` 选择具有特定class的元素：

```css
.highlight {
    background-color: yellow;
}

.text-center {
    text-align: center;
}
```

### 4. ID选择器

使用 `#` 选择具有特定id的元素：

```css
#header {
    background-color: black;
    color: white;
}

#main-content {
    padding: 20px;
}
```

### 5. 属性选择器

根据属性选择元素：

```css
/* 具有title属性的元素 */
[title] {
    cursor: help;
}

/* href属性以https开头的链接 */
[href^="https"] {
    color: green;
}

/* class属性包含"btn"的元素 */
[class*="btn"] {
    padding: 10px;
}

/* href属性以.pdf结尾的链接 */
[href$=".pdf"] {
    background-image: url('pdf-icon.png');
}
```

## 组合选择器

### 1. 后代选择器

选择某元素的所有后代元素：

```css
/* 选择div内的所有p元素 */
div p {
    margin-bottom: 10px;
}

/* 选择article内的所有.highlight元素 */
article .highlight {
    font-weight: bold;
}
```

### 2. 子元素选择器

只选择直接子元素：

```css
/* 选择ul的直接子元素li */
ul > li {
    list-style-type: square;
}

/* 选择nav的直接子元素a */
nav > a {
    text-decoration: none;
}
```

### 3. 相邻兄弟选择器

选择紧接在某元素后的元素：

```css
/* 选择h1后面紧接着的p */
h1 + p {
    font-size: 1.2em;
}

/* 选择div后面紧接着的ul */
div + ul {
    margin-top: 20px;
}
```

### 4. 通用兄弟选择器

选择某元素后的所有兄弟元素：

```css
/* 选择h2后面的所有p */
h2 ~ p {
    color: gray;
}

/* 选择div后面的所有img */
div ~ img {
    border: 1px solid #ccc;
}
```

## 伪类选择器

### 1. 链接状态

```css
/* 未访问的链接 */
a:link {
    color: blue;
}

/* 已访问的链接 */
a:visited {
    color: purple;
}

/* 鼠标悬停 */
a:hover {
    text-decoration: underline;
}

/* 激活状态 */
a:active {
    color: red;
}
```

### 2. 结构伪类

```css
/* 第一个子元素 */
li:first-child {
    font-weight: bold;
}

/* 最后一个子元素 */
li:last-child {
    border-bottom: none;
}

/* 奇数位置的元素 */
tr:nth-child(odd) {
    background-color: #f2f2f2;
}

/* 偶数位置的元素 */
tr:nth-child(even) {
    background-color: #fff;
}

/* 每第3个元素 */
li:nth-child(3n) {
    margin-right: 0;
}
```

### 3. 状态伪类

```css
/* 禁用的输入框 */
input:disabled {
    background-color: #eee;
}

/* 选中的复选框 */
input:checked {
    border-color: blue;
}

/* 获得焦点的输入框 */
input:focus {
    outline: 2px solid blue;
}
```

## 伪元素选择器

### 1. 文本处理

```css
/* 第一行 */
p::first-line {
    font-weight: bold;
}

/* 第一个字母 */
p::first-letter {
    font-size: 2em;
    float: left;
}
```

### 2. 内容插入

```css
/* 在元素之前插入内容 */
.quote::before {
    content: "«";
    color: #666;
}

/* 在元素之后插入内容 */
.quote::after {
    content: "»";
    color: #666;
}
```

## 选择器优先级

### 1. 优先级计算规则

- 内联样式：1000分
- ID选择器：100分
- 类选择器、属性选择器、伪类：10分
- 元素选择器、伪元素：1分

```css
/* 优先级：1分 */
p {
    color: blue;
}

/* 优先级：10分 */
.text {
    color: red;
}

/* 优先级：100分 */
#header {
    color: green;
}

/* 优先级：11分 (10分 + 1分) */
p.text {
    color: purple;
}
```

### 2. !important

覆盖所有其他样式：

```css
.element {
    color: red !important;  /* 这个颜色会优先生效 */
}
```

## 最佳实践

### 1. 选择器性能

- 避免过度嵌套
- 优先使用类选择器
- 避免通用选择器作为关键选择器

```css
/* 不推荐 */
div > * > span > a {
    color: blue;
}

/* 推荐 */
.nav-link {
    color: blue;
}
```

### 2. 可维护性

- 使用有意义的类名
- 保持选择器的简单性
- 避免过度依赖层级关系

```css
/* 不推荐 */
div.container div.content div.sidebar ul li a {
    color: blue;
}

/* 推荐 */
.sidebar-link {
    color: blue;
}
```

### 3. 命名约定

- 使用语义化的命名
- 采用一致的命名规范
- 使用BEM或其他命名方法论

```css
/* BEM命名示例 */
.block__element--modifier {
    property: value;
}

.card__title--large {
    font-size: 24px;
}
```

## 实践技巧

### 1. 组合使用

```css
/* 组合多个选择器 */
.btn:hover,
.btn:focus {
    background-color: #0056b3;
}

/* 特定上下文中的样式 */
.dark-theme .btn {
    background-color: #343a40;
}
```

### 2. 选择器性能优化

```css
/* 避免过度复杂的选择器 */
/* 不推荐 */
html body .wrapper .container .content .article p {
    color: #333;
}

/* 推荐 */
.article-text {
    color: #333;
}
```

## 总结

掌握CSS选择器可以：
- 精确控制页面样式
- 提高样式代码的可维护性
- 优化选择器性能
- 实现复杂的样式需求
