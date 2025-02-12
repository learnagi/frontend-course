---
title: "CSS Flexbox布局"
slug: "css-flexbox"
sequence: 10
description: "掌握CSS Flexbox弹性布局的核心概念和应用"
is_published: true
estimated_minutes: 40
language: "zh-CN"
---

# CSS Flexbox布局

## Flexbox基础

### 1. 容器属性

创建Flex容器：

```css
.flex-container {
    display: flex;         /* 块级弹性容器 */
    /* 或 */
    display: inline-flex;  /* 内联弹性容器 */
}
```

### 2. 主轴方向

控制主轴方向：

```css
.flex-container {
    flex-direction: row;            /* 默认，从左到右 */
    /* 或 */
    flex-direction: row-reverse;    /* 从右到左 */
    /* 或 */
    flex-direction: column;         /* 从上到下 */
    /* 或 */
    flex-direction: column-reverse; /* 从下到上 */
}
```

### 3. 换行控制

```css
.flex-container {
    flex-wrap: nowrap;       /* 默认，不换行 */
    /* 或 */
    flex-wrap: wrap;         /* 允许换行 */
    /* 或 */
    flex-wrap: wrap-reverse; /* 换行并反转 */
}
```

## 对齐和分布

### 1. 主轴对齐

```css
.flex-container {
    justify-content: flex-start;    /* 起点对齐 */
    /* 或 */
    justify-content: flex-end;      /* 终点对齐 */
    /* 或 */
    justify-content: center;        /* 居中对齐 */
    /* 或 */
    justify-content: space-between; /* 两端对齐 */
    /* 或 */
    justify-content: space-around;  /* 环绕对齐 */
    /* 或 */
    justify-content: space-evenly;  /* 均匀对齐 */
}
```

### 2. 交叉轴对齐

```css
.flex-container {
    align-items: stretch;     /* 默认，拉伸填充 */
    /* 或 */
    align-items: flex-start;  /* 起点对齐 */
    /* 或 */
    align-items: flex-end;    /* 终点对齐 */
    /* 或 */
    align-items: center;      /* 居中对齐 */
    /* 或 */
    align-items: baseline;    /* 基线对齐 */
}
```

### 3. 多行对齐

```css
.flex-container {
    align-content: flex-start;    /* 起点对齐 */
    /* 或 */
    align-content: flex-end;      /* 终点对齐 */
    /* 或 */
    align-content: center;        /* 居中对齐 */
    /* 或 */
    align-content: space-between; /* 两端对齐 */
    /* 或 */
    align-content: space-around;  /* 环绕对齐 */
    /* 或 */
    align-content: stretch;       /* 拉伸填充 */
}
```

## Flex项目属性

### 1. 排序

```css
.flex-item {
    order: 0;  /* 默认值 */
    /* 或 */
    order: 1;  /* 更高的值排在后面 */
    /* 或 */
    order: -1; /* 更低的值排在前面 */
}
```

### 2. 弹性增长

```css
.flex-item {
    flex-grow: 0;  /* 默认值，不增长 */
    /* 或 */
    flex-grow: 1;  /* 按比例增长 */
    /* 或 */
    flex-grow: 2;  /* 增长比例是其他项目的2倍 */
}
```

### 3. 弹性收缩

```css
.flex-item {
    flex-shrink: 1;  /* 默认值，允许收缩 */
    /* 或 */
    flex-shrink: 0;  /* 禁止收缩 */
    /* 或 */
    flex-shrink: 2;  /* 收缩比例是其他项目的2倍 */
}
```

### 4. 基准尺寸

```css
.flex-item {
    flex-basis: auto;   /* 默认值 */
    /* 或 */
    flex-basis: 0;      /* 完全依赖flex-grow */
    /* 或 */
    flex-basis: 200px;  /* 指定基准尺寸 */
}
```

### 5. 简写属性

```css
.flex-item {
    /* flex: flex-grow flex-shrink flex-basis */
    flex: 0 1 auto;  /* 默认值 */
    /* 或 */
    flex: 1;         /* 等于 flex: 1 1 0 */
    /* 或 */
    flex: auto;      /* 等于 flex: 1 1 auto */
    /* 或 */
    flex: none;      /* 等于 flex: 0 0 auto */
}
```

## 常见布局模式

### 1. 居中对齐

```css
/* 完全居中 */
.center {
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
}

/* 水平居中 */
.horizontal-center {
    display: flex;
    justify-content: center;
}

/* 垂直居中 */
.vertical-center {
    display: flex;
    align-items: center;
}
```

### 2. 导航栏

```css
/* 基本导航栏 */
.navbar {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1rem;
}

/* 响应式导航栏 */
@media (max-width: 768px) {
    .navbar {
        flex-direction: column;
    }
}
```

### 3. 卡片网格

```css
/* 弹性卡片网格 */
.card-grid {
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
}

.card {
    flex: 1 1 300px;  /* 最小300px，可增长和收缩 */
    max-width: calc(33.333% - 20px);  /* 最多3列 */
}
```

## 高级技巧

### 1. 自动边距对齐

```css
/* 推到右侧 */
.push-right {
    margin-left: auto;
}

/* 推到左侧 */
.push-left {
    margin-right: auto;
}

/* 水平居中单个项目 */
.center-item {
    margin: 0 auto;
}
```

### 2. 嵌套Flex容器

```css
/* 复杂布局 */
.complex-layout {
    display: flex;
}

.sidebar {
    flex: 0 0 200px;
}

.main-content {
    flex: 1;
    display: flex;
    flex-direction: column;
}

.main-content > * {
    margin: 10px;
}
```

### 3. 响应式布局

```css
/* 响应式Flex布局 */
.responsive-layout {
    display: flex;
    flex-wrap: wrap;
}

.responsive-item {
    flex: 1 1 300px;
}

@media (max-width: 768px) {
    .responsive-layout {
        flex-direction: column;
    }
    
    .responsive-item {
        flex: none;
    }
}
```

## 最佳实践

### 1. 性能优化

```css
/* 避免频繁改变flex-basis */
.optimized-item {
    flex: 0 0 auto;
    width: 200px;  /* 使用width代替flex-basis */
}

/* 使用transform代替flex属性进行动画 */
.animated-item {
    transform: scale(1);
    transition: transform 0.3s;
}
```

### 2. 浏览器兼容性

```css
/* 添加浏览器前缀 */
.flex-container {
    display: -webkit-flex;
    display: -ms-flexbox;
    display: flex;
}

/* 回退方案 */
.fallback {
    float: left;  /* 为不支持Flex的浏览器提供回退 */
}

@supports (display: flex) {
    .fallback {
        float: none;
        display: flex;
    }
}
```

### 3. 可维护性

```css
/* 使用CSS变量 */
:root {
    --flex-gap: 20px;
    --flex-column-width: 300px;
}

.flex-grid {
    display: flex;
    flex-wrap: wrap;
    gap: var(--flex-gap);
}

.flex-column {
    flex: 1 1 var(--flex-column-width);
}
```

## 总结

掌握Flexbox布局可以：
- 创建灵活的响应式布局
- 简化复杂的对齐需求
- 实现动态内容布局
- 提高开发效率

Flexbox是现代Web布局的重要工具，它提供了强大而灵活的布局能力，特别适合构建响应式界面和组件。
