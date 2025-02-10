---
title: "HTML5 完全指南"
slug: "html5-complete-guide"
sequence: 1
description: "系统掌握HTML5核心概念、语义化标签、表单应用、多媒体处理等重要特性"
is_published: true
estimated_minutes: 120
language: "zh-CN"
---

# HTML5 完全指南

## 本节概要

通过本节学习，你将学会：
- 掌握HTML5的核心概念和基本结构
- 使用语义化标签构建清晰的文档结构
- 创建交互式表单并进行数据验证
- 集成音频、视频等多媒体内容

💡 重点内容：
- 文档结构与语义化标签
- 表单控件与数据验证
- 多媒体元素的使用
- HTML5新特性实践

## 1. 文档基本结构

基础HTML5模板：
```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>HTML5文档</title>
</head>
<body>
    <!-- 页面内容 -->
</body>
</html>
```

实践：创建一个基础页面模板，添加必要的meta标签和标题。

## 2. 常用标签

文本标签：
```html
<h1>一级标题</h1>
<p>这是一个段落</p>
<strong>重要文本</strong>
<em>强调文本</em>
```

列表标签：
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

链接和图片：
```html
<a href="https://example.com">链接文本</a>
<img src="image.jpg" alt="图片描述">
```

实践：创建一个包含各类标签的个人介绍页面。

## 3. 语义化布局

页面结构：
```html
<header>
    <h1>网站标题</h1>
    <nav>导航菜单</nav>
</header>

<main>
    <article>
        <h2>文章标题</h2>
        <p>文章内容</p>
    </article>
    <aside>侧边栏内容</aside>
</main>

<footer>
    <p>页脚信息</p>
</footer>
```

实践：使用语义化标签重构一个博客首页。

## 4. 表单控件

基础表单：
```html
<form action="/submit" method="post">
    <div class="form-item">
        <label for="username">用户名：</label>
        <input type="text" id="username" name="username" required>
    </div>
    
    <div class="form-item">
        <label for="email">邮箱：</label>
        <input type="email" id="email" name="email" required>
    </div>
    
    <button type="submit">提交</button>
</form>
```

新型输入控件：
```html
<input type="date" value="2025-02-10">
<input type="time">
<input type="color">
<input type="range" min="0" max="100">
<input type="number" min="0" max="100">
```

实践：创建一个完整的用户注册表单。

## 5. 多媒体元素

视频播放器：
```html
<video controls width="640" height="360">
    <source src="video.mp4" type="video/mp4">
    <source src="video.webm" type="video/webm">
    您的浏览器不支持视频播放。
</video>
```

音频播放器：
```html
<audio controls>
    <source src="audio.mp3" type="audio/mpeg">
    <source src="audio.ogg" type="audio/ogg">
    您的浏览器不支持音频播放。
</audio>
```

实践：创建一个包含视频和音频的媒体播放页面。

## 6. 综合实战

创建一个个人博客首页，要求：
1. 使用语义化标签构建页面结构
2. 包含导航菜单和文章列表
3. 添加图片和多媒体内容
4. 实现一个评论表单
5. 注意移动端适配

示例代码：
```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>我的博客</title>
</head>
<body>
    <header>
        <h1>我的博客</h1>
        <nav>
            <a href="#home">首页</a>
            <a href="#articles">文章</a>
            <a href="#about">关于</a>
        </nav>
    </header>

    <main>
        <article>
            <h2>最新文章标题</h2>
            <time datetime="2025-02-10">2025年2月10日</time>
            <p>文章摘要...</p>
            <img src="article-image.jpg" alt="文章配图">
        </article>

        <section id="comments">
            <h2>评论</h2>
            <form id="comment-form">
                <textarea name="comment" required></textarea>
                <button type="submit">发表评论</button>
            </form>
        </section>
    </main>

    <footer>
        <p> 2025 我的博客. All rights reserved.</p>
    </footer>
</body>
</html>
```

## 7. 扩展资源

- [HTML5 MDN文档](https://developer.mozilla.org/zh-CN/docs/Web/HTML)
- [HTML5 标准规范](https://html.spec.whatwg.org/)
- [Can I Use](https://caniuse.com/) - 特性兼容性查询

## 下节预告

下一节：CSS核心概念
- 选择器和样式规则
- 盒模型和布局
- 响应式设计
- 动画效果
