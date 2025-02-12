---
title: "CSS定位"
slug: "css-positioning"
sequence: 8
description: "掌握CSS定位技术，实现精确的元素布局"
is_published: true
estimated_minutes: 35
language: "zh-CN"
---

# CSS 定位

## position 属性

### 1. static（静态定位）

默认定位方式：

```css
.static-element {
    position: static;
    /* top, right, bottom, left 属性无效 */
}
```

### 2. relative（相对定位）

相对于元素原本位置进行定位：

```css
.relative-element {
    position: relative;
    top: 20px;     /* 向下移动20px */
    left: 30px;    /* 向右移动30px */
    /* 原位置会被保留 */
}
```

### 3. absolute（绝对定位）

相对于最近的非static定位祖先元素定位：

```css
.container {
    position: relative;  /* 作为定位上下文 */
}

.absolute-element {
    position: absolute;
    top: 0;
    right: 0;
    /* 脱离文档流 */
}
```

### 4. fixed（固定定位）

相对于视口定位：

```css
.fixed-header {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    /* 固定在视口位置 */
}
```

### 5. sticky（粘性定位）

基于用户的滚动位置定位：

```css
.sticky-nav {
    position: sticky;
    top: 0;
    /* 滚动到顶部时固定 */
}
```

## 定位上下文

### 1. 定位容器

创建定位上下文：

```css
.positioning-context {
    position: relative;
    /* 或 */
    position: absolute;
    /* 或 */
    position: fixed;
}

.child {
    position: absolute;
    /* 相对于最近的定位上下文定位 */
}
```

### 2. 堆叠上下文

控制元素的层叠顺序：

```css
.stacking-context {
    /* 创建新的堆叠上下文 */
    position: relative;
    z-index: 1;
}

.overlay {
    position: absolute;
    z-index: 100;  /* 更高的层级 */
}

.background {
    position: absolute;
    z-index: -1;   /* 更低的层级 */
}
```

## 常见应用场景

### 1. 固定导航栏

```css
.fixed-nav {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    background: white;
    box-shadow: 0 2px 5px rgba(0,0,0,0.1);
    z-index: 1000;
}

/* 为固定导航腾出空间 */
body {
    padding-top: 60px;
}
```

### 2. 模态框

```css
.modal-overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0,0,0,0.5);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 1000;
}

.modal-content {
    position: relative;
    background: white;
    padding: 20px;
    border-radius: 4px;
    max-width: 500px;
    width: 90%;
}
```

### 3. 下拉菜单

```css
.dropdown {
    position: relative;
}

.dropdown-content {
    position: absolute;
    top: 100%;
    left: 0;
    display: none;
    min-width: 200px;
    background: white;
    box-shadow: 0 2px 5px rgba(0,0,0,0.2);
}

.dropdown:hover .dropdown-content {
    display: block;
}
```

### 4. 工具提示

```css
.tooltip-container {
    position: relative;
}

.tooltip {
    position: absolute;
    bottom: 100%;
    left: 50%;
    transform: translateX(-50%);
    padding: 5px 10px;
    background: black;
    color: white;
    border-radius: 4px;
    font-size: 12px;
    white-space: nowrap;
    visibility: hidden;
    opacity: 0;
    transition: opacity 0.3s;
}

.tooltip-container:hover .tooltip {
    visibility: visible;
    opacity: 1;
}
```

## 高级技巧

### 1. 居中定位

```css
/* 绝对定位居中 */
.absolute-center {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}

/* 固定定位居中 */
.fixed-center {
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}
```

### 2. 全屏覆盖

```css
.fullscreen {
    position: fixed;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    /* 或使用简写 */
    inset: 0;
}
```

### 3. 响应式定位

```css
.responsive-element {
    position: relative;
    
    @media (max-width: 768px) {
        position: static;
    }
}

.mobile-fixed {
    @media (max-width: 768px) {
        position: fixed;
        bottom: 0;
        width: 100%;
    }
}
```

## 最佳实践

### 1. 性能优化

```css
/* 使用transform代替定位来实现动画 */
.animated-element {
    position: absolute;
    transform: translateY(0);
    transition: transform 0.3s;
}

.animated-element:hover {
    transform: translateY(-10px);
}
```

### 2. 可访问性

```css
/* 确保固定定位元素不会遮挡内容 */
.skip-link {
    position: absolute;
    top: -40px;
    left: 0;
    background: #000;
    color: white;
    padding: 8px;
    z-index: 100;
}

.skip-link:focus {
    top: 0;
}
```

### 3. 维护性

```css
:root {
    --header-height: 60px;
    --z-index-header: 1000;
    --z-index-modal: 2000;
}

.header {
    position: fixed;
    height: var(--header-height);
    z-index: var(--z-index-header);
}

.modal {
    position: fixed;
    z-index: var(--z-index-modal);
}
```

## 常见问题和解决方案

### 1. 定位失效

```css
/* 确保父元素创建定位上下文 */
.parent {
    position: relative;
    /* 或检查z-index是否正确 */
    z-index: auto;
}
```

### 2. 层叠问题

```css
/* 使用z-index管理层叠顺序 */
.base-layer { z-index: 1; }
.middle-layer { z-index: 2; }
.top-layer { z-index: 3; }

/* 创建新的堆叠上下文 */
.stacking-context {
    position: relative;
    z-index: 0;
    isolation: isolate;
}
```

## 总结

掌握CSS定位可以：
- 创建复杂的页面布局
- 实现交互式界面元素
- 控制元素的层叠顺序
- 优化用户体验
