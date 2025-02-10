---
title: "HTML基础知识"
slug: "html-fundamentals"
sequence: 2
description: "掌握HTML的基本元素和属性，学习网页结构的构建方法"
is_published: true
estimated_minutes: 30
language: "zh-CN"
---

# HTML基础知识

![HTML基础元素](./images/html-fundamentals.png)
*掌握HTML基础，构建网页结构的基石*

## 本节概要

通过本节学习，你将学会：
- 理解HTML元素的基本概念
- 掌握常用HTML标签的使用
- 学习HTML属性的应用
- 创建基础的网页结构

💡 重点内容：
- HTML元素的语法规则
- 常用标签的正确使用
- 属性的设置方法
- 嵌套规则和文档结构

## 1. HTML元素基础

HTML元素的基本构成：
```html
<标签名 属性名="属性值">内容</标签名>
```

常见的元素类型：
- 块级元素（如 `<div>`、`<p>`）
- 内联元素（如 `<span>`、`<a>`）
- 空元素（如 `<img>`、`<br>`）

## 2. 基本页面结构

```html
<!DOCTYPE html>
<html>
<head>
    <!-- 文档头部信息 -->
    <meta charset="UTF-8">
    <title>页面标题</title>
</head>
<body>
    <!-- 页面内容 -->
    <h1>主标题</h1>
    <p>段落内容</p>
</body>
</html>
```

## 3. 常用标签示例

### 文本标签
```html
<h1>一级标题</h1>
<h2>二级标题</h2>
<p>这是一个段落</p>
<span>内联文本</span>
```

### 链接和图片
```html
<a href="https://example.com">访问链接</a>
<img src="image.jpg" alt="图片描述">
```

### 列表
```html
<ul>
    <li>无序列表项</li>
    <li>无序列表项</li>
</ul>

<ol>
    <li>有序列表项1</li>
    <li>有序列表项2</li>
</ol>
```

## 4. HTML属性

常用属性示例：
```html
<!-- 链接属性 -->
<a href="url" target="_blank" title="提示文本">链接</a>

<!-- 图片属性 -->
<img src="image.jpg" alt="替代文本" width="300" height="200">

<!-- 表单属性 -->
<input type="text" name="username" required placeholder="请输入用户名">
```

## 5. 实战练习

创建一个简单的个人介绍页面：

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <title>个人介绍</title>
</head>
<body>
    <h1>关于我</h1>
    
    <img src="avatar.jpg" alt="我的照片" width="200">
    
    <h2>基本信息</h2>
    <ul>
        <li>姓名：张三</li>
        <li>职业：Web开发者</li>
        <li>所在地：北京</li>
    </ul>
    
    <h2>联系方式</h2>
    <p>邮箱：<a href="mailto:example@email.com">example@email.com</a></p>
    
    <h2>个人简介</h2>
    <p>热爱编程，专注Web开发，擅长HTML、CSS和JavaScript。</p>
</body>
</html>
```

## 6. 常见问题

1. 块级元素和内联元素的区别？
   - 块级元素独占一行，可设置宽高
   - 内联元素在行内显示，宽高由内容决定

2. HTML5新增了哪些语义化标签？
   - `<header>`、`<nav>`、`<main>`、`<article>`等
   - 使文档结构更清晰，更利于SEO

3. 为什么要写alt属性？
   - 图片无法显示时的替代文本
   - 帮助屏幕阅读器识别图片内容
   - 有利于SEO优化

## 下节预告

下一节：[HTML层级结构](./03-html-hierarchy.md)
- 文档对象模型（DOM）
- 元素嵌套规则
- 文档结构最佳实践
