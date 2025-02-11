---
title: "HTML段落元素"
slug: "html-paragraphs"
sequence: 5
description: "掌握HTML段落元素的使用，学习文本格式化和段落布局技巧"
is_published: true
estimated_minutes: 25
language: "zh-CN"
---

# HTML段落元素

![HTML段落格式](./images/html-paragraphs.png)
*掌握段落排版，提升文档可读性*

## 本节概要

通过本节学习，你将学会：
- 使用段落标签组织文本内容
- 掌握文本格式化技巧
- 控制段落间距和布局
- 理解段落与其他元素的关系

💡 重点内容：
- 段落标签的使用
- 文本格式化
- 空白处理
- 段落布局技巧

## 1. 段落基础

### 基本语法
```html
<p>这是一个段落。段落标签会自动在其前后创建一些空白。</p>
<p>这是另一个段落。注意段落之间的间距。</p>
```

### 空白处理
HTML会将连续的空白字符合并为一个空格：

```html
<p>这段文字    中间有很多    空格，
    还有换行，但是在浏览器中
    会被合并为一个空格。</p>
```

## 2. 文本格式化

### 基本格式化
```html
<p>这是<strong>重要</strong>的文本。</p>
<p>这是<em>强调</em>的文本。</p>
<p>这是<mark>高亮</mark>的文本。</p>
<p>这是<small>小号</small>的文本。</p>
```

### 特殊字符
```html
<p>HTML中的特殊字符：</p>
<p>&lt; 小于号</p>
<p>&gt; 大于号</p>
<p>&amp; 和号</p>
<p>&quot; 引号</p>
<p>&copy; 版权符号</p>
```

## 3. 段落布局

### 文本对齐
使用CSS控制段落对齐方式：

```html
<style>
.text-left { text-align: left; }
.text-center { text-align: center; }
.text-right { text-align: right; }
.text-justify { text-align: justify; }
</style>

<p class="text-left">左对齐文本</p>
<p class="text-center">居中文本</p>
<p class="text-right">右对齐文本</p>
<p class="text-justify">两端对齐文本，这段文本较长，可以看到两端对齐的效果。为了演示效果，我们需要足够多的文字。</p>
```

### 段落间距
使用CSS控制段落间距：

```html
<style>
p {
    margin-bottom: 1.5em; /* 段落下方间距 */
    line-height: 1.6;    /* 行高 */
}
</style>
```

## 4. 段落与其他元素

### 段落中的内联元素
```html
<p>
    段落中可以包含
    <a href="#">链接</a>、
    <strong>重要文本</strong>、
    <em>强调文本</em>和
    <span>普通内联元素</span>。
</p>
```

### 段落与块级元素
```html
<!-- 正确：段落在div中 -->
<div>
    <p>这是一个段落</p>
</div>

<!-- 错误：段落中不能包含div -->
<p>
    <div>这是错误的嵌套</div>
</p>
```

## 5. 实战练习

创建一个格式丰富的文章页面：

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <title>文章排版示例</title>
    <style>
        body {
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
            line-height: 1.6;
        }
        
        p {
            margin-bottom: 1.5em;
        }
        
        .highlight {
            background-color: #fff3d4;
            padding: 20px;
            border-radius: 5px;
        }
        
        .quote {
            border-left: 4px solid #ccc;
            padding-left: 20px;
            font-style: italic;
        }
    </style>
</head>
<body>
    <article>
        <h1>文章标题</h1>
        
        <p class="highlight">
            这是文章的导语，用来概括主要内容。导语通常会使用特殊的样式来吸引读者注意。
        </p>
        
        <p>
            这是正文第一段，包含了<strong>重要信息</strong>和<em>需要强调的内容</em>。
            段落之间有适当的间距，确保文章结构清晰。
        </p>
        
        <p class="quote">
            这是一段引用文字，使用了不同的样式来区分普通段落。
            ——作者署名
        </p>
        
        <p>
            这是最后一段，用来总结文章内容。注意观察段落之间的间距、行高等排版细节。
        </p>
    </article>
</body>
</html>
```

## 6. 常见问题

1. 为什么段落间的空白行会被忽略？
   - HTML会合并连续的空白字符
   - 使用margin控制间距

2. 如何保留文本格式？
   - 使用 `<pre>` 标签
   - 使用 CSS white-space 属性

3. 段落中能否使用块级元素？
   - 不能，段落中只能包含内联元素
   - 需要块级元素时，应该在段落外使用

## 下节预告

下一节：[HTML属性](./06-html-attributes.md)
- 常用HTML属性
- 属性的语法规则
- 自定义数据属性
