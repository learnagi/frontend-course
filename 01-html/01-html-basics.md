---
title: "HTML基础入门"
slug: "html-basics"
sequence: 1
description: "了解HTML5基础概念，掌握文档结构，配置开发环境"
is_published: true
estimated_minutes: 30
language: "zh-CN"
---

# HTML基础入门

![HTML基础概念](./images/html-basics-intro.png)
*开启HTML5学习之旅，构建网页基础*

## 本节概要

通过本节学习，你将学会：
- 理解HTML5的基本概念和发展历史
- 掌握HTML文档的基本结构和元素组成
- 配置高效的前端开发环境
- 编写第一个HTML页面

💡 重点内容：
- HTML5的新特性和改进
- 文档类型声明和元素结构
- 开发工具的选择和配置

## 1. HTML5简介

HTML5是HTML最新的修订版本，广泛应用于现代Web开发。它引入了许多新特性：

- 语义化标签（header、nav、footer等）
- 增强的表单控件
- 原生音视频支持
- Canvas绘图
- 本地存储功能

## 2. 文档基本结构

一个标准的HTML5文档结构：

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>我的第一个HTML5页面</title>
</head>
<body>
    <h1>欢迎学习HTML5</h1>
    <p>这是一个基础的HTML5页面结构。</p>
</body>
</html>
```

📝 代码说明：
- `<!DOCTYPE html>` 声明文档类型
- `<html>` 是根元素
- `<head>` 包含元数据
- `<body>` 包含可见内容

## 3. 开发工具配置

推荐的开发工具：

1. 代码编辑器
   - Visual Studio Code
   - Sublime Text
   - WebStorm

2. 必备插件
   - HTML CSS Support
   - Live Server
   - Auto Close Tag
   - HTML Snippets

3. 浏览器开发工具
   - Chrome DevTools
   - Firefox Developer Tools

## 4. 实战练习

创建你的第一个HTML页面：

1. 新建文件 `index.html`
2. 添加基本文档结构
3. 在body中添加以下内容：
   - 标题
   - 段落
   - 图片
   - 链接

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>我的个人主页</title>
</head>
<body>
    <h1>欢迎来到我的主页</h1>
    <p>这是我的第一个HTML页面。</p>
    <img src="avatar.jpg" alt="我的头像">
    <a href="about.html">关于我</a>
</body>
</html>
```

## 5. 常见问题解答

1. 文档类型声明是否必须？
   - 是的，它告诉浏览器使用哪个HTML版本

2. 为什么需要设置viewport？
   - 确保页面在移动设备上正确显示

3. charset设置的作用？
   - 定义文档的字符编码，通常使用UTF-8

## 下节预告

下一节：[常用HTML标签](./02-html-tags.md)
- 文本标签的使用
- 列表的创建和嵌套
- 链接和图片的插入
