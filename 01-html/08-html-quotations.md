---
title: "HTML引用元素"
slug: "html-quotations"
sequence: 8
description: "掌握HTML引用元素的使用，学习如何正确引用和标注内容来源"
is_published: true
estimated_minutes: 20
language: "zh-CN"
---

# HTML引用元素

![HTML引用元素](./images/html-quotations.png)
*正确使用引用元素，规范内容引用*

## 本节概要

通过本节学习，你将学会：
- 使用块级引用和行内引用
- 添加引文来源和作者信息
- 创建缩写和定义列表
- 掌握引用的最佳实践

💡 重点内容：
- 块级引用
- 行内引用
- 引文标注
- 缩写定义

## 1. 块级引用

### 基本用法
```html
<blockquote>
    <p>这是一段长引用文本，通常用于引用较长的内容。</p>
</blockquote>
```

### 添加来源
```html
<blockquote cite="https://example.com/source">
    <p>这是引用的内容。</p>
    <footer>
        <cite>——作者名称</cite>
    </footer>
</blockquote>
```

## 2. 行内引用

### 短引用
```html
<p>正如某人所说：<q>这是一段短引用</q>。</p>

<p>这本书的作者写道：<q cite="https://example.com/book">引用的内容</q></p>
```

### 引文组合
```html
<p>
    <q>知识就是力量</q>
    <cite>——弗朗西斯·培根</cite>
</p>
```

## 3. 缩写和定义

### 缩写
```html
<p>
    <abbr title="World Wide Web">WWW</abbr>
    <abbr title="HyperText Markup Language">HTML</abbr>
</p>
```

### 定义列表
```html
<dl>
    <dt>HTML</dt>
    <dd>超文本标记语言，用于创建网页的标准标记语言。</dd>
    
    <dt>CSS</dt>
    <dd>层叠样式表，用于定义HTML文档样式的语言。</dd>
</dl>
```

## 4. 实战练习

创建一个包含各种引用的文章页面：

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <title>名人名言集锦</title>
    <style>
        body {
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
            line-height: 1.6;
        }
        
        blockquote {
            margin: 20px 0;
            padding: 20px;
            background-color: #f9f9f9;
            border-left: 5px solid #ccc;
        }
        
        blockquote footer {
            margin-top: 10px;
            font-style: italic;
        }
        
        q {
            color: #666;
        }
        
        dl {
            background-color: #f5f5f5;
            padding: 20px;
            border-radius: 5px;
        }
        
        dt {
            font-weight: bold;
            color: #333;
        }
        
        dd {
            margin-left: 20px;
            margin-bottom: 10px;
        }
        
        abbr {
            text-decoration: underline dotted;
            cursor: help;
        }
    </style>
</head>
<body>
    <article>
        <h1>经典引言集</h1>
        
        <section>
            <h2>名人名言</h2>
            
            <blockquote cite="https://example.com/einstein">
                <p>想象力比知识更重要。知识是有限的，而想象力概括着世界的一切，推动着进步，并且是知识进化的源泉。</p>
                <footer>
                    <cite>——阿尔伯特·爱因斯坦</cite>
                </footer>
            </blockquote>
            
            <p>
                正如苏格拉底所说：<q>未经检验的人生不值得过。</q>
                这句话启发了无数后人。
            </p>
        </section>
        
        <section>
            <h2>技术术语</h2>
            
            <dl>
                <dt><abbr title="HyperText Markup Language">HTML</abbr></dt>
                <dd>网页开发的基础语言，用于构建网页的结构。</dd>
                
                <dt><abbr title="Cascading Style Sheets">CSS</abbr></dt>
                <dd>用于定义网页样式和布局的语言。</dd>
                
                <dt><abbr title="JavaScript">JS</abbr></dt>
                <dd>一种脚本语言，用于创建动态网页内容。</dd>
            </dl>
        </section>
        
        <section>
            <h2>经典书籍摘录</h2>
            
            <blockquote cite="https://example.com/book">
                <p>代码就像是写给人看的，附带能在机器上运行。</p>
                <footer>
                    <cite>——《代码大全》</cite>
                </footer>
            </blockquote>
        </section>
    </article>
</body>
</html>
```

## 5. 最佳实践

1. 引用规范
   - 使用适当的引用标签
   - 添加来源信息
   - 正确标注作者

2. 缩写使用
   - 首次出现时提供完整说明
   - 使用title属性提供解释
   - 考虑上下文的理解性

3. 定义列表
   - 合理组织术语和定义
   - 保持结构清晰
   - 适当使用样式

## 6. 检查清单

- [ ] 引用内容使用适当的标签
- [ ] 添加了必要的来源信息
- [ ] 正确使用cite属性和标签
- [ ] 缩写有明确的说明
- [ ] 定义列表结构清晰
- [ ] 页面布局美观易读

## 下节预告

下一节：[HTML注释](./09-html-comments.md)
- 注释的语法和用途
- 注释的最佳实践
- 条件注释的使用
