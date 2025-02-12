---
title: "CSS高级主题"
slug: "css-advanced-topics"
sequence: 16
description: "探索CSS的高级特性和新兴技术"
is_published: true
estimated_minutes: 45
language: "zh-CN"
---

# CSS高级主题

## CSS变量（自定义属性）

### 1. 变量定义和使用

```css
:root {
    /* 全局变量 */
    --primary-color: #3498db;
    --secondary-color: #2ecc71;
    --spacing-unit: 8px;
}

.component {
    /* 局部变量 */
    --component-padding: 20px;
    
    /* 使用变量 */
    color: var(--primary-color);
    padding: var(--component-padding);
    
    /* 提供默认值 */
    margin: var(--margin, 10px);
}
```

### 2. 动态变量

```css
/* 基于媒体查询更新变量 */
:root {
    --font-size-base: 16px;
}

@media (min-width: 768px) {
    :root {
        --font-size-base: 18px;
    }
}

/* JavaScript操作变量 */
.dynamic {
    --x: 0;
    --y: 0;
    transform: translate(var(--x), var(--y));
}
```

## 容器查询

### 1. 基本用法

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

/* 容器相对单位 */
.container-item {
    font-size: 2cqi; /* 相对于容器内联大小的2% */
}
```

### 2. 高级用法

```css
/* 多重容器查询 */
@container (min-width: 400px) and (min-height: 300px) {
    .responsive-element {
        /* 样式 */
    }
}

/* 样式查询 */
@container style(--theme: dark) {
    .theme-aware {
        /* 暗色主题样式 */
    }
}
```

## CSS Houdini

### 1. Paint API

```css
/* 注册自定义画笔 */
CSS.paintWorklet.addModule('myPaint.js');

/* 使用自定义画笔 */
.element {
    background-image: paint(myPaint);
}
```

### 2. Properties and Values API

```css
/* 注册自定义属性 */
@property --gradient-angle {
    syntax: '<angle>';
    initial-value: 0deg;
    inherits: false;
}

/* 使用自定义属性 */
.gradient {
    background: linear-gradient(var(--gradient-angle), blue, red);
    animation: rotate 1s linear infinite;
}

@keyframes rotate {
    to {
        --gradient-angle: 360deg;
    }
}
```

## CSS模块

### 1. CSS Modules

```css
/* style.module.css */
.button {
    background: var(--primary-color);
}

.button:hover {
    opacity: 0.9;
}

/* 组合样式 */
.primaryButton {
    composes: button;
    color: white;
}
```

### 2. CSS-in-JS

```javascript
// styled-components示例
const Button = styled.button`
    background: ${props => props.primary ? 'blue' : 'gray'};
    padding: 10px 20px;
    border-radius: 4px;
    
    &:hover {
        opacity: 0.9;
    }
`;
```

## 新特性

### 1. 逻辑属性

```css
.logical-layout {
    /* 逻辑尺寸 */
    inline-size: 200px;
    block-size: 100px;
    
    /* 逻辑边距 */
    margin-block-start: 1em;
    margin-inline-end: 2em;
    
    /* 逻辑边框 */
    border-inline: 1px solid;
    
    /* 逻辑位置 */
    inset-block-start: 0;
}
```

### 2. 滚动捕捉

```css
.scroll-container {
    /* 启用滚动捕捉 */
    scroll-snap-type: x mandatory;
    overflow-x: scroll;
}

.scroll-item {
    /* 定义捕捉点 */
    scroll-snap-align: start;
    
    /* 设置捕捉边距 */
    scroll-margin: 1rem;
}
```

### 3. 子网格

```css
.grid-container {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
}

.grid-item {
    /* 继承父网格的列线 */
    display: grid;
    grid-template-columns: subgrid;
}
```

## 实验性特性

### 1. 嵌套规则

```css
/* 原生CSS嵌套 */
.card {
    background: white;
    
    & .header {
        color: blue;
        
        & h2 {
            margin: 0;
        }
    }
    
    &:hover {
        box-shadow: 0 2px 4px rgba(0,0,0,0.1);
    }
}
```

### 2. 范围查询

```css
/* @scope规则 */
@scope (.card) {
    :scope {
        /* 卡片根元素样式 */
    }
    
    .title {
        /* 仅影响.card内的.title */
    }
}
```

### 3. 层叠层

```css
/* 定义层叠层 */
@layer framework, custom;

@layer framework {
    button {
        /* 框架样式 */
    }
}

@layer custom {
    button {
        /* 自定义样式，优先级更高 */
    }
}
```

## 性能和可访问性

### 1. 内容可见性

```css
.content-visibility {
    /* 自动跳过渲染屏幕外内容 */
    content-visibility: auto;
    
    /* 预留空间以防止布局偏移 */
    contain-intrinsic-size: 0 500px;
}
```

### 2. 减少布局偏移

```css
.stable-layout {
    /* 预留空间 */
    min-height: 100px;
    
    /* 使用aspect-ratio预防偏移 */
    aspect-ratio: 16 / 9;
    
    /* 固定尺寸图片 */
    img {
        width: 100%;
        height: auto;
    }
}
```

### 3. 焦点管理

```css
.focus-visible {
    /* 仅在键盘导航时显示焦点轮廓 */
    &:focus-visible {
        outline: 2px solid blue;
        outline-offset: 2px;
    }
    
    /* 自定义焦点指示器 */
    &:focus {
        outline: none;
        box-shadow: 0 0 0 3px rgba(66, 153, 225, 0.5);
    }
}
```

## 总结

现代CSS的高级特性可以：
- 提供更强大的样式控制
- 改善代码组织和维护
- 优化性能和用户体验
- 增强可访问性和可用性
- 简化复杂布局的实现

随着浏览器不断发展，新的CSS特性会持续增加，保持学习和实践很重要。
