---
title: "HTML与CSS"
slug: "html-css"
sequence: 11
description: "学习HTML与CSS的基础知识，掌握网页样式设计的核心概念"
is_published: true
estimated_minutes: 45
language: "zh-CN"
---

# HTML与CSS

![HTML与CSS](./images/html-css.png)
*掌握HTML与CSS的结合，创建精美的网页设计*

## 本节概要

通过本节学习，你将学会：
- 理解CSS的基本概念
- 掌握CSS选择器的使用
- 学习CSS样式属性
- 理解CSS盒模型

💡 重点内容：
- CSS语法和使用方式
- 选择器类型和优先级
- 常用样式属性
- 盒模型概念
- 布局基础

## 1. CSS简介

### 什么是CSS
CSS（层叠样式表）用于定义HTML元素的显示方式，控制网页的布局和外观。

### CSS语法
```css
选择器 {
    属性: 值;
    属性: 值;
}
```

## 2. CSS使用方式

### 内联样式
直接在HTML元素中使用style属性：
```html
<p style="color: blue; font-size: 16px;">这是内联样式</p>
```

### 内部样式
在HTML文档头部使用style标签：
```html
<style>
    p {
        color: blue;
        font-size: 16px;
    }
</style>
```

### 外部样式
通过link标签引入外部CSS文件：
```html
<link rel="stylesheet" href="styles.css">
```

## 3. CSS选择器

### 基本选择器
```css
/* 元素选择器 */
p { color: blue; }

/* 类选择器 */
.highlight { background-color: yellow; }

/* ID选择器 */
#header { font-size: 24px; }

/* 通用选择器 */
* { margin: 0; padding: 0; }
```

### 组合选择器
```css
/* 后代选择器 */
div p { color: red; }

/* 子元素选择器 */
div > p { color: blue; }

/* 相邻兄弟选择器 */
h1 + p { margin-top: 20px; }

/* 通用兄弟选择器 */
h1 ~ p { color: gray; }
```

### 伪类和伪元素
```css
/* 伪类 */
a:hover { color: red; }
li:first-child { font-weight: bold; }

/* 伪元素 */
p::first-line { color: blue; }
p::before { content: "→"; }
```

## 4. CSS常用属性

### 文本样式
```css
p {
    color: #333;
    font-family: Arial, sans-serif;
    font-size: 16px;
    font-weight: bold;
    text-align: center;
    line-height: 1.5;
    text-decoration: underline;
}
```

### 背景样式
```css
div {
    background-color: #f0f0f0;
    background-image: url('bg.jpg');
    background-repeat: no-repeat;
    background-position: center;
    background-size: cover;
}
```

### 边框和圆角
```css
.box {
    border: 1px solid #ccc;
    border-radius: 5px;
    box-shadow: 2px 2px 5px rgba(0,0,0,0.1);
}
```

## 5. CSS盒模型

### 盒模型组成
```css
.box {
    /* 内容区域 */
    width: 200px;
    height: 100px;
    
    /* 内边距 */
    padding: 20px;
    
    /* 边框 */
    border: 1px solid black;
    
    /* 外边距 */
    margin: 10px;
}
```

### 盒模型类型
```css
/* 标准盒模型 */
.box-standard {
    box-sizing: content-box;
}

/* IE盒模型 */
.box-border {
    box-sizing: border-box;
}
```

## 6. CSS布局基础

### 显示属性
```css
.element {
    display: block;
    display: inline;
    display: inline-block;
    display: flex;
    display: grid;
}
```

### 定位
```css
.positioned {
    position: relative;
    position: absolute;
    position: fixed;
    position: sticky;
    
    top: 0;
    left: 0;
    z-index: 1;
}
```

### Flexbox布局
```css
.container {
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-wrap: wrap;
}

.item {
    flex: 1;
}
```

## 练习
### 1. 创建导航栏
创建一个响应式导航栏，包含logo和菜单项：

```html
<!-- HTML结构 -->
<nav class="navbar">
    <div class="logo">
        <img src="logo.png" alt="Logo">
    </div>
    <ul class="nav-links">
        <li><a href="#home">首页</a></li>
        <li><a href="#about">关于</a></li>
        <li><a href="#services">服务</a></li>
        <li><a href="#contact">联系我们</a></li>
    </ul>
</nav>
```

```css
/* 导航栏样式 */
.navbar {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1rem 2rem;
    background-color: #ffffff;
    box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

.logo img {
    height: 40px;
}

.nav-links {
    display: flex;
    list-style: none;
    margin: 0;
    padding: 0;
}

.nav-links li {
    margin-left: 2rem;
}

.nav-links a {
    text-decoration: none;
    color: #333;
    font-weight: 500;
    transition: color 0.3s ease;
}

.nav-links a:hover {
    color: #007bff;
}

/* 响应式设计 */
@media (max-width: 768px) {
    .nav-links {
        display: none;
    }
}
```

### 2. 设计卡片组件
创建一个现代化的卡片组件，包含图片、标题和描述：

```html
<!-- HTML结构 -->
<div class="card">
    <div class="card-image">
        <img src="image.jpg" alt="Card Image">
    </div>
    <div class="card-content">
        <h3 class="card-title">卡片标题</h3>
        <p class="card-description">这是一段卡片描述文本，可以包含多行内容。</p>
        <button class="card-button">了解更多</button>
    </div>
</div>
```

```css
/* 卡片样式 */
.card {
    width: 300px;
    border-radius: 8px;
    overflow: hidden;
    box-shadow: 0 4px 8px rgba(0,0,0,0.1);
    transition: transform 0.3s ease;
}

.card:hover {
    transform: translateY(-5px);
}

.card-image img {
    width: 100%;
    height: 200px;
    object-fit: cover;
}

.card-content {
    padding: 1.5rem;
}

.card-title {
    margin: 0 0 1rem 0;
    color: #333;
    font-size: 1.25rem;
}

.card-description {
    color: #666;
    line-height: 1.5;
    margin-bottom: 1.5rem;
}

.card-button {
    display: inline-block;
    padding: 0.5rem 1rem;
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.3s ease;
}

.card-button:hover {
    background-color: #0056b3;
}
```

### 3. 实现响应式布局
创建一个响应式的网格布局系统：

```html
<!-- HTML结构 -->
<div class="grid-container">
    <div class="grid-item">1</div>
    <div class="grid-item">2</div>
    <div class="grid-item">3</div>
    <div class="grid-item">4</div>
    <div class="grid-item">5</div>
    <div class="grid-item">6</div>
</div>
```

```css
/* 网格布局样式 */
.grid-container {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 20px;
    padding: 20px;
}

.grid-item {
    background-color: #f8f9fa;
    padding: 20px;
    border-radius: 4px;
    text-align: center;
    box-shadow: 0 2px 4px rgba(0,0,0,0.05);
}

/* 响应式布局 */
@media (max-width: 768px) {
    .grid-container {
        grid-template-columns: repeat(2, 1fr);
    }
}

@media (max-width: 480px) {
    .grid-container {
        grid-template-columns: 1fr;
    }
}
```

这些练习示例展示了：
1. 现代化的导航栏设计
2. 交互式卡片组件
3. 响应式网格布局

每个示例都包含了：
- 完整的HTML结构
- 详细的CSS样式
- 响应式设计考虑
- 交互效果（悬停、过渡等）

## 小结
- CSS是控制网页样式的核心技术
- 选择器决定样式应用的范围
- 盒模型是布局的基础
- 灵活运用各种属性可以创建丰富的页面效果

## 扩展阅读
- [MDN CSS教程](https://developer.mozilla.org/zh-CN/docs/Web/CSS)
- [CSS-Tricks](https://css-tricks.com/)