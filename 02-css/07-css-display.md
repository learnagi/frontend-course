---
title: "CSS显示属性"
slug: "css-display"
sequence: 7
description: "深入理解CSS显示属性及其应用"
is_published: true
estimated_minutes: 30
language: "zh-CN"
---

# CSS 显示属性

## display 属性基础

### 1. 块级元素 (block)

占据父容器的整行空间：

```css
.block-element {
    display: block;
    width: 80%;
    margin: 10px auto;
}

/* 常见的块级元素 */
div, p, h1, section {
    /* 默认display: block */
}
```

### 2. 内联元素 (inline)

在行内显示，不会打断文本流：

```css
.inline-element {
    display: inline;
    /* width和height属性无效 */
    padding: 0 10px;
}

/* 常见的内联元素 */
span, a, strong, em {
    /* 默认display: inline */
}
```

### 3. 内联块元素 (inline-block)

结合了块级和内联元素的特性：

```css
.inline-block-element {
    display: inline-block;
    width: 100px;
    height: 100px;
    margin: 10px;
}
```

## 特殊显示值

### 1. none

完全隐藏元素：

```css
.hidden {
    display: none;  /* 元素不占用空间 */
}

/* 常见用途 */
@media (max-width: 768px) {
    .desktop-only {
        display: none;
    }
}
```

### 2. flex

创建弹性布局容器：

```css
.flex-container {
    display: flex;
    justify-content: space-between;
    align-items: center;
}
```

### 3. grid

创建网格布局容器：

```css
.grid-container {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 20px;
}
```

### 4. table 相关

表格布局属性：

```css
.table-layout {
    display: table;
    width: 100%;
}

.table-row {
    display: table-row;
}

.table-cell {
    display: table-cell;
    padding: 10px;
}
```

## 可见性控制

### 1. visibility

控制元素可见性但保留空间：

```css
.invisible {
    visibility: hidden;  /* 隐藏但保留空间 */
}

.visible {
    visibility: visible;  /* 显示元素 */
}
```

### 2. opacity

控制元素透明度：

```css
.transparent {
    opacity: 0;  /* 完全透明 */
}

.semi-transparent {
    opacity: 0.5;  /* 半透明 */
}

.fully-visible {
    opacity: 1;  /* 完全不透明 */
}
```

## 溢出控制

### 1. overflow

控制内容溢出：

```css
.container {
    /* 自动添加滚动条 */
    overflow: auto;
    
    /* 隐藏溢出内容 */
    overflow: hidden;
    
    /* 始终显示滚动条 */
    overflow: scroll;
    
    /* 单独控制方向 */
    overflow-x: hidden;
    overflow-y: auto;
}
```

### 2. text-overflow

文本溢出处理：

```css
.text-truncate {
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
}

/* 多行文本截断 */
.multiline-truncate {
    display: -webkit-box;
    -webkit-line-clamp: 3;
    -webkit-box-orient: vertical;
    overflow: hidden;
}
```

## 布局技巧

### 1. 居中对齐

```css
/* 水平居中 */
.horizontal-center {
    display: block;
    margin: 0 auto;
}

/* 文本居中 */
.text-center {
    text-align: center;
}

/* 完全居中 */
.absolute-center {
    display: flex;
    justify-content: center;
    align-items: center;
}
```

### 2. 列表布局

```css
/* 移除列表样式 */
.clean-list {
    list-style: none;
    padding: 0;
    margin: 0;
}

/* 水平列表 */
.horizontal-list {
    display: flex;
    gap: 20px;
}

/* 网格列表 */
.grid-list {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
    gap: 20px;
}
```

### 3. 响应式显示

```css
/* 响应式显示控制 */
@media (max-width: 768px) {
    .hide-mobile {
        display: none;
    }
    
    .stack-mobile {
        display: block;
    }
}

@media (min-width: 769px) {
    .hide-desktop {
        display: none;
    }
    
    .inline-desktop {
        display: inline-block;
    }
}
```

## 实践应用

### 1. 导航栏

```css
.nav {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1rem;
}

@media (max-width: 768px) {
    .nav {
        flex-direction: column;
    }
    
    .nav-menu {
        display: none;
    }
    
    .nav-menu.active {
        display: flex;
        flex-direction: column;
    }
}
```

### 2. 卡片网格

```css
.card-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 20px;
    padding: 20px;
}

.card {
    display: flex;
    flex-direction: column;
    overflow: hidden;
}
```

### 3. 模态框

```css
.modal {
    display: none;
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.5);
}

.modal.active {
    display: flex;
    justify-content: center;
    align-items: center;
}
```

## 最佳实践

### 1. 语义化显示

```css
/* 使用适当的HTML元素和显示属性 */
article {
    display: block;
}

nav ul {
    display: flex;
}

button {
    display: inline-block;
}
```

### 2. 性能考虑

```css
/* 使用transform代替display:none进行动画 */
.fade-element {
    opacity: 0;
    transform: scale(0.95);
    transition: opacity 0.3s, transform 0.3s;
}

.fade-element.active {
    opacity: 1;
    transform: scale(1);
}
```

### 3. 可访问性

```css
/* 隐藏元素但保持可访问性 */
.visually-hidden {
    position: absolute;
    width: 1px;
    height: 1px;
    padding: 0;
    margin: -1px;
    overflow: hidden;
    clip: rect(0, 0, 0, 0);
    border: 0;
}
```

## 总结

掌握CSS显示属性可以：
- 控制元素的布局行为
- 创建响应式设计
- 实现复杂的界面布局
- 优化用户体验
