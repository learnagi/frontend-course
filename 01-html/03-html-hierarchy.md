---
title: "HTML层级结构"
slug: "html-hierarchy"
sequence: 3
description: "深入理解HTML文档的层级结构，掌握DOM树的概念和元素嵌套规则"
is_published: true
estimated_minutes: 25
language: "zh-CN"
---

# HTML层级结构

![HTML层级结构](./images/html-hierarchy.png)
*理解HTML文档的层级关系，构建清晰的文档结构*

## 本节概要

通过本节学习，你将学会：
- 理解DOM树的概念和结构
- 掌握HTML元素的嵌套规则
- 学习文档结构的最佳实践
- 避免常见的结构错误

💡 重点内容：
- DOM树的基本概念
- 元素嵌套规则
- 文档结构规范
- 常见错误避免

## 1. DOM树结构

文档对象模型（DOM）将HTML文档表示为树形结构：

```html
<!DOCTYPE html>
<html>
    <head>
        <title>网页标题</title>
    </head>
    <body>
        <header>
            <h1>主标题</h1>
            <nav>
                <ul>
                    <li><a href="#">链接1</a></li>
                    <li><a href="#">链接2</a></li>
                </ul>
            </nav>
        </header>
        <main>
            <article>
                <h2>文章标题</h2>
                <p>文章内容</p>
            </article>
        </main>
    </body>
</html>
```

## 2. 元素嵌套规则

### 基本规则
- 块级元素可以包含块级和内联元素
- 内联元素通常只能包含其他内联元素
- 某些元素有特定的内容模型

### 常见的嵌套关系
```html
<!-- 正确的嵌套 -->
<div>
    <p>段落中的<span>重点</span>内容</p>
</div>

<!-- 错误的嵌套 -->
<p>
    <div>不应该在p标签中嵌套div</div>
</p>
```

## 3. 语义化结构

推荐的页面结构：
```html
<header>
    <nav>导航内容</nav>
</header>

<main>
    <article>
        <section>
            <h2>章节标题</h2>
            <p>章节内容</p>
        </section>
    </article>
    
    <aside>
        <h3>侧边栏</h3>
        <ul>
            <li>相关链接</li>
        </ul>
    </aside>
</main>

<footer>
    <p>页脚信息</p>
</footer>
```

## 4. 常见错误示例

### 1. 标签未正确闭合
```html
<!-- 错误示例 -->
<div>
    <p>这是一个段落
</div>

<!-- 正确示例 -->
<div>
    <p>这是一个段落</p>
</div>
```

### 2. 属性引号缺失
```html
<!-- 错误示例 -->
<img src=image.jpg alt=图片>

<!-- 正确示例 -->
<img src="image.jpg" alt="图片">
```

### 3. 标签大小写混用
```html
<!-- 不推荐 -->
<DIV>
    <P>内容</P>
</DIV>

<!-- 推荐 -->
<div>
    <p>内容</p>
</div>
```

## 5. 实战练习

创建一个具有清晰层级结构的新闻页面：

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <title>新闻网站</title>
</head>
<body>
    <header>
        <h1>每日新闻</h1>
        <nav>
            <ul>
                <li><a href="#home">首页</a></li>
                <li><a href="#news">新闻</a></li>
                <li><a href="#contact">联系我们</a></li>
            </ul>
        </nav>
    </header>

    <main>
        <article>
            <header>
                <h2>重要新闻标题</h2>
                <time datetime="2025-02-10">2025年2月10日</time>
            </header>
            
            <section>
                <h3>新闻详情</h3>
                <p>新闻内容段落...</p>
                <figure>
                    <img src="news-image.jpg" alt="新闻图片">
                    <figcaption>图片说明</figcaption>
                </figure>
            </section>
        </article>

        <aside>
            <h3>相关新闻</h3>
            <ul>
                <li><a href="#">相关新闻1</a></li>
                <li><a href="#">相关新闻2</a></li>
            </ul>
        </aside>
    </main>

    <footer>
        <p>版权所有 © 2025</p>
    </footer>
</body>
</html>
```

## 6. 检查清单

- [ ] 文档类型声明正确
- [ ] HTML标签嵌套合理
- [ ] 标签都正确闭合
- [ ] 使用了适当的语义化标签
- [ ] 属性格式规范
- [ ] 代码缩进清晰

## 下节预告

下一节：[HTML标题元素](./04-html-headings.md)
- 标题层级的正确使用
- SEO优化考虑
- 标题最佳实践
