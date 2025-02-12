---
title: "CSS默认样式详解"
slug: "css-default"
sequence: 1
description: "深入理解CSS默认样式，掌握样式重置和规范化技术"
is_published: true
estimated_minutes: 45
language: "zh-CN"
---

# CSS 入门指南

## CSS 简介

CSS（层叠样式表）是用于控制网页样式和布局的语言。它允许你对网页元素进行样式设置，包括颜色、大小、间距、定位等。

## CSS 语法

CSS 规则由选择器和声明块组成：

```css
selector {
    property1: value1;
    property2: value2;
}
```

例如：
```css
h1 {
    color: blue;
    font-size: 20px;
}
```

## CSS 选择器

### 1. 基本选择器

- **元素选择器**：直接使用元素名
  ```css
  p { color: red; }
  ```

- **类选择器**：使用 `.` 前缀
  ```css
  .highlight { background-color: yellow; }
  ```

- **ID 选择器**：使用 `#` 前缀
  ```css
  #header { background-color: black; }
  ```

### 2. 组合选择器

- **后代选择器**：使用空格
  ```css
  div p { color: blue; }
  ```

- **子元素选择器**：使用 `>`
  ```css
  div > p { color: green; }
  ```

- **相邻兄弟选择器**：使用 `+`
  ```css
  h1 + p { margin-top: 20px; }
  ```

### 3. 分组选择器

用逗号分隔多个选择器：
```css
h1, h2, h3 { 
    font-family: Arial; 
}
```

## 如何添加 CSS

### 1. 内联样式（Inline CSS）

直接在 HTML 元素中使用 style 属性：

```html
<p style="color: red; font-size: 16px;">这是一段文本</p>
```

### 2. 内部样式表（Internal CSS）

在 HTML 文件的 `<head>` 部分使用 `<style>` 标签：

```html
<head>
    <style>
        p {
            color: blue;
            font-size: 16px;
        }
    </style>
</head>
```

### 3. 外部样式表（External CSS）

创建单独的 CSS 文件并在 HTML 中引用：

```html
<head>
    <link rel="stylesheet" type="text/css" href="styles.css">
</head>
```

## CSS 优先级

样式的优先级从高到低：

1. 内联样式（Inline styles）
2. 内部和外部样式表（根据顺序）
3. 浏览器默认样式

### 优先级计算规则：

- 内联样式：1000 分
- ID 选择器：100 分
- 类选择器、属性选择器、伪类：10 分
- 元素选择器、伪元素：1 分

## 多个样式表

当多个样式表包含同一个元素的规则时：

1. **外部样式表**
```html
<link rel="stylesheet" type="text/css" href="styles.css">
```

2. **多个外部样式表**
```html
<link rel="stylesheet" type="text/css" href="base.css">
<link rel="stylesheet" type="text/css" href="theme.css">
```

后引入的样式表优先级更高（在没有更高特异性的情况下）。

### 样式表优先级顺序（从高到低）：

1. 内联样式
2. 内部样式表（在 `<head>` 标签内）
3. 外部样式表
4. 浏览器默认样式

## CSS 默认样式详解

### 什么是默认样式？

浏览器的默认样式（User Agent Stylesheet）是浏览器内置的基础 CSS 样式，用于定义 HTML 元素在没有自定义样式时的基本外观。

### 常见的默认样式

1. **边距和填充**
   - `body` 元素默认有 8px 外边距
   - 标题和段落有默认的上下外边距
   - 列表有默认的左内边距

2. **文本样式**
   - 默认字体大小为 16px
   - 标题元素有默认的大小和粗细
   - 链接默认为蓝色且有下划线

3. **显示属性**
   - 块级元素默认占据整行
   - 内联元素默认在同一行显示

### 重置默认样式

#### 1. Reset CSS

完全重置所有默认样式：

```css
* {
    margin: 0;
    padding: 0;
    border: 0;
    font-size: 100%;
    font: inherit;
    vertical-align: baseline;
}
```

#### 2. Normalize.css

保留有用的默认样式，修复浏览器差异：

```css
html {
    line-height: 1.15;
    -webkit-text-size-adjust: 100%;
}

body {
    margin: 0;
}
```

## 最佳实践

1. **样式组织**
   - 使用清晰的命名约定
   - 按组件或功能组织 CSS
   - 避免过度嵌套选择器

2. **性能优化**
   - 避免使用过于复杂的选择器
   - 合理使用继承
   - 适当使用 CSS 压缩

3. **维护性**
   - 编写注释说明复杂的样式规则
   - 保持代码风格一致
   - 定期检查和清理未使用的样式

## 常见问题和解决方案

1. **CSS 特异性冲突**
   - 使用更具体的选择器
   - 适当使用 `!important`（谨慎使用）
   - 遵循命名规范

2. **跨浏览器兼容性**
   - 使用 CSS 预处理器
   - 添加适当的浏览器前缀
   - 测试主流浏览器

3. **响应式设计**
   - 使用媒体查询
   - 采用弹性布局
   - 使用相对单位

## 总结

CSS 是前端开发中不可或缺的技术，掌握好 CSS 的基础知识和最佳实践，可以：
- 创建美观的用户界面
- 提高代码可维护性
- 优化网页性能
- 提供更好的用户体验
