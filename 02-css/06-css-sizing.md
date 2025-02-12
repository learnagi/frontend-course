---
title: "CSS尺寸与边距"
slug: "css-sizing"
sequence: 6
description: "深入理解CSS中的尺寸单位和边距控制"
is_published: true
estimated_minutes: 35
language: "zh-CN"
---

# CSS 尺寸与边距

## CSS 尺寸单位

### 1. 绝对单位

固定大小，不受其他因素影响：

```css
.element {
    /* 像素 */
    width: 100px;
    
    /* 英寸 */
    margin: 1in;
    
    /* 厘米 */
    padding: 2cm;
    
    /* 毫米 */
    border-width: 3mm;
    
    /* 点 */
    font-size: 12pt;
}
```

### 2. 相对单位

相对于其他值计算大小：

```css
.element {
    /* 相对于根元素字体大小 */
    width: 10rem;
    
    /* 相对于父元素字体大小 */
    margin: 2em;
    
    /* 相对于字符'x'的高度 */
    padding: 3ex;
    
    /* 相对于视口宽度 */
    max-width: 80vw;
    
    /* 相对于视口高度 */
    height: 50vh;
    
    /* 相对于视口大小的较小值 */
    font-size: 5vmin;
    
    /* 相对于视口大小的较大值 */
    margin: 2vmax;
}
```

### 3. 百分比单位

相对于父元素的尺寸：

```css
.element {
    /* 宽度为父元素的80% */
    width: 80%;
    
    /* 高度为父元素的50% */
    height: 50%;
    
    /* 内边距相对于父元素宽度 */
    padding: 5%;
    
    /* 外边距相对于父元素宽度 */
    margin: 10%;
}
```

## 尺寸属性

### 1. 基本尺寸

```css
.element {
    /* 宽度和高度 */
    width: 300px;
    height: 200px;
    
    /* 最小尺寸 */
    min-width: 100px;
    min-height: 100px;
    
    /* 最大尺寸 */
    max-width: 800px;
    max-height: 600px;
}
```

### 2. 内部尺寸

```css
.element {
    /* 内容区域尺寸 */
    width: fit-content;
    height: fit-content;
    
    /* 根据内容自动调整 */
    width: auto;
    height: auto;
}
```

### 3. 宽高比

```css
.element {
    /* 保持宽高比 */
    aspect-ratio: 16/9;
    width: 100%;
    
    /* 正方形 */
    aspect-ratio: 1;
}
```

## 边距控制

### 1. 外边距（Margin）

```css
.element {
    /* 所有边距相同 */
    margin: 20px;
    
    /* 上下、左右 */
    margin: 20px 40px;
    
    /* 上、左右、下 */
    margin: 20px 40px 30px;
    
    /* 上、右、下、左 */
    margin: 20px 40px 30px 10px;
    
    /* 负边距 */
    margin-top: -20px;
    
    /* 自动边距（用于水平居中） */
    margin: 0 auto;
}
```

### 2. 内边距（Padding）

```css
.element {
    /* 所有内边距相同 */
    padding: 20px;
    
    /* 上下、左右 */
    padding: 20px 40px;
    
    /* 上、左右、下 */
    padding: 20px 40px 30px;
    
    /* 上、右、下、左 */
    padding: 20px 40px 30px 10px;
    
    /* 单独设置 */
    padding-top: 20px;
    padding-right: 40px;
    padding-bottom: 30px;
    padding-left: 10px;
}
```

## 响应式尺寸

### 1. 视口相关单位

```css
.responsive-element {
    /* 视口宽度 */
    width: 90vw;
    max-width: 1200px;
    
    /* 视口高度 */
    height: 80vh;
    
    /* 最小值 */
    font-size: 3vmin;
    
    /* 最大值 */
    padding: 2vmax;
}
```

### 2. 弹性尺寸

```css
.flexible-element {
    /* 弹性宽度 */
    width: clamp(200px, 50%, 800px);
    
    /* 弹性字体大小 */
    font-size: clamp(16px, 2vw, 24px);
    
    /* 弹性边距 */
    margin: clamp(10px, 3%, 30px);
}
```

### 3. 计算值

```css
.calculated-element {
    /* 计算宽度 */
    width: calc(100% - 40px);
    
    /* 混合单位计算 */
    margin: calc(2rem + 20px);
    
    /* 复杂计算 */
    padding: calc((100vw - 1200px) / 2);
}
```

## 特殊技巧

### 1. 等比例盒子

```css
.aspect-box {
    /* 16:9 比例 */
    width: 100%;
    padding-top: 56.25%;
    position: relative;
}

.aspect-box > * {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
}
```

### 2. 内容限制

```css
.content-box {
    /* 限制内容宽度 */
    max-width: 65ch;
    margin: 0 auto;
    
    /* 文本截断 */
    width: 100%;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
}
```

### 3. 动态间距

```css
.dynamic-spacing {
    /* 根据视口大小调整间距 */
    padding: clamp(1rem, 5vw, 3rem);
    
    /* 响应式间距 */
    gap: min(2vw, 20px);
}
```

## 最佳实践

### 1. 移动优先

```css
.responsive-container {
    /* 基础样式（移动端） */
    width: 100%;
    padding: 1rem;
    
    /* 平板 */
    @media (min-width: 768px) {
        padding: 2rem;
        max-width: 720px;
        margin: 0 auto;
    }
    
    /* 桌面 */
    @media (min-width: 1024px) {
        padding: 3rem;
        max-width: 960px;
    }
}
```

### 2. 可维护性

```css
:root {
    /* 定义全局尺寸变量 */
    --spacing-unit: 8px;
    --container-width: 1200px;
    --content-width: 65ch;
}

.element {
    /* 使用变量 */
    padding: calc(var(--spacing-unit) * 2);
    max-width: var(--container-width);
    margin: 0 auto;
}
```

### 3. 性能优化

```css
.optimized-element {
    /* 使用transform代替width/height动画 */
    transform: scale(1);
    transition: transform 0.3s;
    
    /* 避免布局抖动 */
    min-height: 200px;
}
```

## 总结

掌握CSS尺寸与边距可以：
- 创建灵活的响应式布局
- 精确控制元素大小和间距
- 提高用户界面的一致性
- 优化移动端体验
