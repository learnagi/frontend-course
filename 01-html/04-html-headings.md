---
title: "HTML标题元素"
slug: "html-headings"
sequence: 4
description: "掌握HTML标题元素的使用，了解标题层级结构和SEO最佳实践"
is_published: true
estimated_minutes: 20
language: "zh-CN"
---

# HTML标题元素

![HTML标题层级](./images/html-headings.png)
*掌握标题层级，构建清晰的文档结构*

## 本节概要

通过本节学习，你将学会：
- 理解HTML标题元素的重要性
- 掌握六个级别标题的正确使用
- 学习标题层级对SEO的影响
- 实践标题的最佳使用方式

💡 重点内容：
- 标题层级结构
- SEO最佳实践
- 标题的语义化使用
- 常见错误避免

## 1. 标题基础

HTML提供六个级别的标题：

```html
<h1>一级标题</h1>
<h2>二级标题</h2>
<h3>三级标题</h3>
<h4>四级标题</h4>
<h5>五级标题</h5>
<h6>六级标题</h6>
```

## 2. 标题使用规则

### 层级规则
```html
<h1>网站名称</h1>
<section>
    <h2>主要章节</h2>
    <article>
        <h3>文章标题</h3>
        <h4>文章子标题</h4>
    </article>
</section>
```

### 常见错误
```html
<!-- 错误：跳级使用 -->
<h1>主标题</h1>
<h4>子标题</h4>  <!-- 不应该跳过h2和h3 -->

<!-- 错误：多个h1 -->
<h1>第一个主标题</h1>
<h1>第二个主标题</h1>  <!-- 一个页面通常只需要一个h1 -->
```

## 3. SEO考虑

标题对SEO的影响：
- `<h1>` 是最重要的SEO信号之一
- 每个页面应该只有一个 `<h1>`
- 标题要包含关键词
- 保持层级结构清晰

```html
<!-- SEO友好的标题结构 -->
<h1>Web开发教程 - HTML标题元素</h1>
<h2>什么是HTML标题？</h2>
<h2>为什么标题很重要？</h2>
<h3>对SEO的影响</h3>
<h3>对用户体验的影响</h3>
```

## 4. 标题样式

虽然可以通过CSS修改标题样式，但不应该仅仅为了视觉效果而使用特定级别的标题：

```html
<!-- CSS样式示例 -->
<style>
h1 {
    font-size: 2.5em;
    color: #333;
}
h2 {
    font-size: 2em;
    color: #666;
}
h3 {
    font-size: 1.5em;
    color: #999;
}
</style>
```

## 5. 实战练习

创建一个博客文章页面，正确使用标题层级：

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <title>标题层级示例</title>
</head>
<body>
    <header>
        <h1>我的技术博客</h1>
        <nav>
            <h2>导航菜单</h2>
            <ul>
                <li><a href="#home">首页</a></li>
                <li><a href="#articles">文章</a></li>
            </ul>
        </nav>
    </header>

    <main>
        <article>
            <h2>JavaScript基础教程</h2>
            
            <section>
                <h3>变量和数据类型</h3>
                <p>变量是存储数据的容器...</p>
                
                <h4>数值类型</h4>
                <p>JavaScript中的数值类型包括...</p>
                
                <h4>字符串类型</h4>
                <p>字符串用于表示文本数据...</p>
            </section>

            <section>
                <h3>运算符</h3>
                <p>JavaScript提供了多种运算符...</p>
            </section>
        </article>

        <aside>
            <h2>相关文章</h2>
            <ul>
                <li><a href="#">HTML基础</a></li>
                <li><a href="#">CSS入门</a></li>
            </ul>
        </aside>
    </main>

    <footer>
        <h2>页脚信息</h2>
        <p>版权所有 © 2025</p>
    </footer>
</body>
</html>
```

## 6. 检查清单

- [ ] 页面只有一个h1标题
- [ ] 标题层级不跳级使用
- [ ] 标题内容有意义且包含关键词
- [ ] 标题结构清晰易懂
- [ ] 避免过多的标题嵌套

## 下节预告

下一节：[HTML段落元素](./05-html-paragraphs.md)
- 段落的正确使用
- 文本格式化
- 段落间距控制
