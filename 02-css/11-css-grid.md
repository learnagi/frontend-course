---
title: "CSS Grid布局"
slug: "css-grid"
sequence: 11
description: "掌握CSS Grid网格布局系统"
is_published: true
estimated_minutes: 45
language: "zh-CN"
---

# CSS Grid布局

## Grid基础

### 1. 创建网格容器

```css
.grid-container {
    display: grid;          /* 块级网格容器 */
    /* 或 */
    display: inline-grid;   /* 内联网格容器 */
}
```

### 2. 定义网格结构

```css
.grid-container {
    /* 定义列 */
    grid-template-columns: 200px 1fr 2fr;
    
    /* 定义行 */
    grid-template-rows: 100px auto;
    
    /* 使用repeat()函数 */
    grid-template-columns: repeat(3, 1fr);
    
    /* 混合使用固定值和弹性值 */
    grid-template-columns: 200px repeat(2, 1fr);
}
```

### 3. 网格间距

```css
.grid-container {
    /* 设置间距 */
    gap: 20px;              /* 行列间距相同 */
    /* 或 */
    row-gap: 20px;          /* 行间距 */
    column-gap: 30px;       /* 列间距 */
}
```

## 网格线和区域

### 1. 网格线命名

```css
.grid-container {
    grid-template-columns: [start] 1fr [content-start] 2fr [content-end] 1fr [end];
    grid-template-rows: [header] 100px [main] auto [footer] 50px;
}
```

### 2. 定义网格区域

```css
.grid-container {
    grid-template-areas: 
        "header header header"
        "nav    main   aside"
        "footer footer footer";
}

.header { grid-area: header; }
.nav { grid-area: nav; }
.main { grid-area: main; }
.aside { grid-area: aside; }
.footer { grid-area: footer; }
```

## 项目定位

### 1. 使用网格线

```css
.grid-item {
    /* 使用数字 */
    grid-column: 1 / 3;     /* 从第1条列线到第3条列线 */
    grid-row: 2 / 4;        /* 从第2条行线到第4条行线 */
    
    /* 使用命名的网格线 */
    grid-column: start / content-end;
    grid-row: header / main;
    
    /* 使用span关键字 */
    grid-column: span 2;    /* 跨越2列 */
    grid-row: span 3;       /* 跨越3行 */
}
```

### 2. 使用区域

```css
.grid-item {
    /* 指定区域名称 */
    grid-area: header;
    
    /* 使用网格线定义区域 */
    grid-area: 1 / 1 / 2 / 4;  /* 行开始 / 列开始 / 行结束 / 列结束 */
}
```

## 对齐和分布

### 1. 网格项目对齐

```css
.grid-container {
    /* 水平对齐 */
    justify-items: start;    /* 左对齐 */
    justify-items: end;      /* 右对齐 */
    justify-items: center;   /* 居中对齐 */
    justify-items: stretch;  /* 拉伸填充（默认） */
    
    /* 垂直对齐 */
    align-items: start;      /* 顶部对齐 */
    align-items: end;        /* 底部对齐 */
    align-items: center;     /* 居中对齐 */
    align-items: stretch;    /* 拉伸填充（默认） */
}

/* 单个项目对齐 */
.grid-item {
    justify-self: center;
    align-self: center;
}
```

### 2. 网格内容对齐

```css
.grid-container {
    /* 水平对齐整个网格内容 */
    justify-content: start;
    justify-content: end;
    justify-content: center;
    justify-content: space-between;
    justify-content: space-around;
    justify-content: space-evenly;
    
    /* 垂直对齐整个网格内容 */
    align-content: start;
    align-content: end;
    align-content: center;
    align-content: space-between;
    align-content: space-around;
    align-content: space-evenly;
}
```

## 响应式网格

### 1. minmax()函数

```css
.responsive-grid {
    /* 响应式列宽 */
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    
    /* 响应式行高 */
    grid-template-rows: minmax(100px, auto);
}
```

### 2. auto-fit和auto-fill

```css
.auto-fit-grid {
    /* 自适应列数，空间分配给现有列 */
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
}

.auto-fill-grid {
    /* 自适应列数，保留空列 */
    grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
}
```

### 3. 媒体查询

```css
.responsive-layout {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 20px;
    
    @media (max-width: 1200px) {
        grid-template-columns: repeat(3, 1fr);
    }
    
    @media (max-width: 900px) {
        grid-template-columns: repeat(2, 1fr);
    }
    
    @media (max-width: 600px) {
        grid-template-columns: 1fr;
    }
}
```

## 常见布局模式

### 1. 经典布局

```css
/* 圣杯布局 */
.holy-grail {
    display: grid;
    grid-template-areas:
        "header header header"
        "nav    main   aside"
        "footer footer footer";
    grid-template-columns: 200px 1fr 200px;
    grid-template-rows: auto 1fr auto;
    min-height: 100vh;
}

/* 卡片网格 */
.card-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 20px;
    padding: 20px;
}
```

### 2. 特殊布局

```css
/* 交错网格 */
.masonry-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
    grid-auto-rows: 20px;
    grid-auto-flow: dense;
}

.masonry-item {
    grid-row: span attr(data-height);
}

/* 重叠布局 */
.overlap-grid {
    display: grid;
    grid-template: repeat(2, 1fr) / repeat(2, 1fr);
}

.overlap-item {
    grid-area: 1 / 1 / 3 / 3;
    z-index: 1;
}
```

## 高级技巧

### 1. 自动布局

```css
.auto-layout {
    display: grid;
    grid-auto-flow: row dense;  /* 自动填充空隙 */
    grid-auto-rows: minmax(100px, auto);
    grid-auto-columns: minmax(100px, auto);
}
```

### 2. 嵌套网格

```css
.parent-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
}

.nested-grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 10px;
}
```

### 3. 动态网格

```css
.dynamic-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    grid-auto-rows: minmax(100px, auto);
    gap: 20px;
    
    @media (prefers-reduced-motion: no-preference) {
        transition: grid-template-columns 0.3s;
    }
}
```

## 最佳实践

### 1. 性能优化

```css
/* 避免频繁改变网格结构 */
.optimized-grid {
    grid-template-columns: repeat(12, 1fr);
    
    /* 使用grid-area代替改变网格结构 */
    .item {
        grid-area: auto / auto / span 3 / span 4;
    }
}
```

### 2. 可维护性

```css
:root {
    --grid-columns: 12;
    --grid-gap: 20px;
    --grid-min-width: 200px;
}

.maintainable-grid {
    display: grid;
    grid-template-columns: repeat(var(--grid-columns), 1fr);
    gap: var(--grid-gap);
}
```

### 3. 浏览器兼容性

```css
/* 提供回退方案 */
.grid-container {
    display: flex;
    flex-wrap: wrap;
}

@supports (display: grid) {
    .grid-container {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    }
}
```

## 总结

掌握CSS Grid布局可以：
- 创建复杂的二维布局
- 实现响应式设计
- 简化布局代码
- 提高开发效率

Grid布局是现代Web开发中最强大的布局工具之一，它提供了前所未有的布局控制能力。
