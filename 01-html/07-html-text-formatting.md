---
title: "HTML文本格式化"
slug: "html-text-formatting"
sequence: 7
description: "掌握HTML文本格式化标签的使用，学习文本样式和排版技巧"
is_published: true
estimated_minutes: 25
language: "zh-CN"
---

# HTML文本格式化

![HTML文本格式化](./images/html-text-formatting.png)
*使用文本格式化标签，提升内容可读性*

## 本节概要

通过本节学习，你将学会：
- 使用HTML文本格式化标签
- 掌握文本样式和排版技巧
- 理解各种格式化标签的语义
- 学习文本格式化最佳实践

💡 重点内容：
- 基本文本格式化
- 语义化标签使用
- 排版技巧
- 格式化最佳实践

## 1. 基本文本格式化

### 文本样式
```html
<strong>重要文本</strong>
<em>强调文本</em>
<mark>高亮文本</mark>
<small>小号文本</small>
<del>删除文本</del>
<ins>插入文本</ins>
<sub>下标</sub>
<sup>上标</sup>
```

### 预格式化文本
```html
<pre>
这是预格式化文本
    它会保留空格
    和换行
就像你在编辑器中看到的那样
</pre>
```

## 2. 语义化文本标签

### 引用和引文
```html
<blockquote>
    <p>这是一段长引用文本。</p>
    <cite>——引用来源</cite>
</blockquote>

<p>这里有一个<q>短引用</q>。</p>
```

### 代码和计算机输出
```html
<code>console.log('Hello World');</code>
<kbd>Ctrl + S</kbd>
<samp>程序输出示例</samp>
<var>变量名</var>
```

## 3. 文本方向和换行

### 文本方向
```html
<p dir="ltr">从左到右的文本</p>
<p dir="rtl">从右到左的文本</p>
<bdo dir="rtl">这段文字会从右到左显示</bdo>
```

### 换行和分隔
```html
<p>第一行<br>第二行</p>
<p>文本之间的<wbr>换行建议</p>
<hr>
```

## 4. 实战练习

创建一个格式丰富的文章页面：

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <title>文本格式化示例</title>
    <style>
        body {
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
            line-height: 1.6;
        }
        
        blockquote {
            border-left: 4px solid #ccc;
            margin: 20px 0;
            padding-left: 20px;
            font-style: italic;
        }
        
        code {
            background-color: #f4f4f4;
            padding: 2px 5px;
            border-radius: 3px;
            font-family: monospace;
        }
        
        .highlight {
            background-color: #fff3d4;
            padding: 2px;
        }
    </style>
</head>
<body>
    <article>
        <h1>HTML文本格式化指南</h1>
        
        <p>在这篇文章中，我们将学习<strong>HTML文本格式化</strong>的重要性。</p>
        
        <h2>为什么需要文本格式化？</h2>
        <p>格式化文本可以：</p>
        <ul>
            <li>提高<em>可读性</em></li>
            <li>突出<mark>重要信息</mark></li>
            <li>创建更好的<small>视觉层次</small></li>
        </ul>
        
        <blockquote>
            <p>好的排版是优秀网页设计的基础。</p>
            <cite>——网页设计指南</cite>
        </blockquote>
        
        <h2>代码示例</h2>
        <p>使用<code>text-align</code>属性可以控制文本对齐方式：</p>
        <pre>
.text-center {
    text-align: center;
}
        </pre>
        
        <p>保存文件请按 <kbd>Ctrl + S</kbd></p>
        
        <h2>科学公式</h2>
        <p>水的化学式是 H<sub>2</sub>O</p>
        <p>2<sup>3</sup> = 8</p>
        
        <h2>文本更新</h2>
        <p>产品价格：<del>¥999</del> <ins>¥899</ins></p>
        
        <hr>
        
        <footer>
            <p><small>© 2025 HTML教程. 保留所有权利。</small></p>
        </footer>
    </article>
</body>
</html>
```

## 5. 常见问题

1. `<strong>` 和 `<b>` 的区别？
   - `<strong>` 表示重要性
   - `<b>` 仅表示视觉上的加粗

2. `<em>` 和 `<i>` 的区别？
   - `<em>` 表示强调
   - `<i>` 表示不同的语气或风格

3. 何时使用 `<pre>` 标签？
   - 需要保留空格和换行时
   - 显示代码块时
   - 展示格式化文本时

## 6. 最佳实践

1. 使用语义化标签
   - 选择有意义的标签
   - 避免纯视觉效果的标签

2. 合理使用格式化
   - 不过度使用格式化
   - 保持一致性
   - 考虑可访问性

3. 注意代码可读性
   - 适当缩进
   - 添加注释
   - 保持结构清晰

## 下节预告

下一节：[HTML引用元素](./08-html-quotations.md)
- 块引用和行内引用
- 引文和来源标注
- 缩写和定义列表
