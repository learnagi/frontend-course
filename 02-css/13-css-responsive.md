---
title: "CSS响应式设计"
slug: "css-responsive"
sequence: 13
description: "学习CSS响应式设计原理和实践"
is_published: true
estimated_minutes: 35
language: "zh-CN"
---

# CSS响应式设计

## 响应式设计基础

### 1. 视口设置

```html
<!-- 在HTML头部设置视口 -->
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

### 2. 相对单位

```css
.responsive-element {
    /* 相对于视口的单位 */
    width: 90vw;
    height: 80vh;
    font-size: 5vmin;
    
    /* 相对于根元素的单位 */
    margin: 2rem;
    padding: 1.5rem;
    
    /* 相对于父元素的单位 */
    width: 80%;
    font-size: 1.2em;
}
```

### 3. 媒体查询

```css
/* 基于屏幕宽度的媒体查询 */
@media screen and (max-width: 768px) {
    /* 移动端样式 */
}

@media screen and (min-width: 769px) and (max-width: 1024px) {
    /* 平板样式 */
}

@media screen and (min-width: 1025px) {
    /* 桌面样式 */
}

/* 基于屏幕方向的媒体查询 */
@media (orientation: portrait) {
    /* 竖屏样式 */
}

@media (orientation: landscape) {
    /* 横屏样式 */
}
```

## 响应式布局技术

### 1. 流式布局

```css
.fluid-layout {
    /* 最大宽度限制 */
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 20px;
    
    /* 流式图片 */
    img {
        max-width: 100%;
        height: auto;
    }
}
```

### 2. 弹性布局

```css
.flexible-container {
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
}

.flexible-item {
    flex: 1 1 300px;  /* 基础大小300px，可伸缩 */
    
    @media (max-width: 600px) {
        flex: 1 1 100%;  /* 移动端占满宽度 */
    }
}
```

### 3. 网格布局

```css
.grid-container {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 20px;
    
    @media (max-width: 768px) {
        grid-template-columns: 1fr;  /* 移动端单列 */
    }
}
```

## 响应式组件

### 1. 响应式导航

```css
.nav {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1rem;
}

.nav-menu {
    display: flex;
    gap: 20px;
}

@media (max-width: 768px) {
    .nav {
        flex-direction: column;
    }
    
    .nav-menu {
        display: none;  /* 默认隐藏 */
        width: 100%;
        flex-direction: column;
    }
    
    .nav-menu.active {
        display: flex;  /* 点击时显示 */
    }
    
    .menu-toggle {
        display: block;  /* 显示汉堡菜单 */
    }
}
```

### 2. 响应式卡片

```css
.card-container {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 20px;
    padding: 20px;
}

.card {
    display: flex;
    flex-direction: column;
    
    /* 响应式图片 */
    img {
        width: 100%;
        height: auto;
        object-fit: cover;
    }
    
    /* 响应式内容 */
    .content {
        padding: clamp(1rem, 3vw, 2rem);
    }
    
    /* 响应式字体 */
    .title {
        font-size: clamp(1.2rem, 4vw, 1.5rem);
    }
}
```

### 3. 响应式表格

```css
.responsive-table {
    width: 100%;
    border-collapse: collapse;
    
    @media (max-width: 768px) {
        /* 移动端表格样式 */
        thead {
            display: none;
        }
        
        tr {
            display: block;
            margin-bottom: 1rem;
            border: 1px solid #ddd;
        }
        
        td {
            display: block;
            text-align: right;
            padding: 0.5rem;
            
            &::before {
                content: attr(data-label);
                float: left;
                font-weight: bold;
            }
        }
    }
}
```

## 响应式图片

### 1. 基本响应式图片

```css
.responsive-image {
    max-width: 100%;
    height: auto;
}

/* 背景图片 */
.responsive-background {
    background-image: url('large.jpg');
    background-size: cover;
    background-position: center;
    
    @media (max-width: 768px) {
        background-image: url('small.jpg');
    }
}
```

### 2. 图片集

```html
<!-- 使用srcset和sizes属性 -->
<img src="default.jpg"
     srcset="small.jpg 300w,
             medium.jpg 600w,
             large.jpg 900w"
     sizes="(max-width: 300px) 100vw,
            (max-width: 600px) 50vw,
            33vw"
     alt="响应式图片">

<!-- 使用picture元素 -->
<picture>
    <source media="(min-width: 900px)" srcset="large.jpg">
    <source media="(min-width: 600px)" srcset="medium.jpg">
    <img src="small.jpg" alt="响应式图片">
</picture>
```

## 响应式排版

### 1. 流式排版

```css
.fluid-typography {
    /* 使用clamp()函数设置响应式字体大小 */
    font-size: clamp(1rem, 2.5vw, 2rem);
    
    /* 响应式行高 */
    line-height: clamp(1.5, 2vw + 1.5, 2);
    
    /* 响应式段落宽度 */
    max-width: 65ch;
    margin: 0 auto;
}
```

### 2. 响应式间距

```css
:root {
    /* 定义响应式间距变量 */
    --space-unit: clamp(1rem, 3vw, 2rem);
}

.responsive-spacing {
    /* 使用响应式间距 */
    padding: var(--space-unit);
    margin-bottom: calc(var(--space-unit) * 2);
    
    /* 响应式间隙 */
    gap: clamp(1rem, 2vw, 2rem);
}
```

## 高级响应式技巧

### 1. 容器查询

```css
/* 定义容器 */
.container {
    container-type: inline-size;
    container-name: sidebar;
}

/* 基于容器宽度的样式 */
@container sidebar (min-width: 400px) {
    .container-item {
        display: grid;
        grid-template-columns: repeat(2, 1fr);
    }
}
```

### 2. 特性查询

```css
/* 检查浏览器特性支持 */
@supports (display: grid) {
    .modern-layout {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    }
}

@supports not (display: grid) {
    .modern-layout {
        display: flex;
        flex-wrap: wrap;
    }
}
```

### 3. 响应式加载

```css
/* 条件加载CSS */
<link rel="stylesheet" 
      href="large.css" 
      media="(min-width: 1024px)">

/* 响应式字体加载 */
@font-face {
    font-family: 'CustomFont';
    src: url('small.woff2') format('woff2');
    font-display: swap;
}

@media (min-width: 1024px) {
    @font-face {
        font-family: 'CustomFont';
        src: url('large.woff2') format('woff2');
        font-display: swap;
    }
}
```

## 最佳实践

### 1. 移动优先

```css
/* 基础样式（移动端） */
.element {
    width: 100%;
    padding: 1rem;
}

/* 平板样式 */
@media (min-width: 768px) {
    .element {
        width: 50%;
        padding: 2rem;
    }
}

/* 桌面样式 */
@media (min-width: 1024px) {
    .element {
        width: 33.333%;
        padding: 3rem;
    }
}
```

### 2. 性能优化

```css
/* 优化媒体查询 */
@media screen and (max-width: 768px) {
    /* 将相关样式组合在一起 */
    .mobile-styles {
        /* 移动端样式 */
    }
}

/* 避免重复代码 */
:root {
    --base-font-size: 16px;
    --scale-ratio: 1.2;
}

.optimized-typography {
    font-size: calc(var(--base-font-size) * var(--scale-ratio));
}
```

### 3. 可维护性

```css
/* 使用CSS变量管理断点 */
:root {
    --breakpoint-sm: 576px;
    --breakpoint-md: 768px;
    --breakpoint-lg: 992px;
    --breakpoint-xl: 1200px;
}

/* 使用混合宏（如果使用预处理器） */
@mixin responsive($breakpoint) {
    @media (min-width: var(--breakpoint-#{$breakpoint})) {
        @content;
    }
}
```

## 总结

掌握响应式设计可以：
- 创建适应不同设备的布局
- 提供最佳的用户体验
- 维护单一代码库
- 提高网站可访问性

响应式设计是现代Web开发的核心技能，需要综合运用多种技术来创建灵活、自适应的网站。
