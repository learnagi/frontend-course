---
title: "CSS盒模型基础"
slug: "css-box-model"
sequence: 5
description: "理解CSS盒模型的概念和应用"
is_published: true
estimated_minutes: 35
language: "zh-CN"
---

# CSS 盒模型基础

## 什么是盒模型？

CSS盒模型是网页布局的基础，它定义了每个HTML元素如何占据空间以及元素之间如何相互作用。每个元素都被视为一个矩形盒子，包含以下部分：

- Content（内容）：显示实际内容的区域
- Padding（内边距）：内容周围的空白区域
- Border（边框）：包围内边距和内容的边界
- Margin（外边距）：元素外部的空白区域

## 盒模型类型

### 1. 标准盒模型（content-box）

```css
.standard-box {
    box-sizing: content-box;  /* 默认值 */
    width: 200px;            /* 内容区域宽度 */
    padding: 20px;           /* 内边距 */
    border: 1px solid #000;  /* 边框 */
    margin: 10px;           /* 外边距 */
}
```

实际宽度计算：
- 总宽度 = width + padding-left + padding-right + border-left + border-right
- 总高度 = height + padding-top + padding-bottom + border-top + border-bottom

### 2. IE盒模型（border-box）

```css
.border-box {
    box-sizing: border-box;
    width: 200px;           /* 包含padding和border的总宽度 */
    padding: 20px;
    border: 1px solid #000;
    margin: 10px;
}
```

实际宽度计算：
- 内容区域宽度 = width - padding-left - padding-right - border-left - border-right
- 内容区域高度 = height - padding-top - padding-bottom - border-top - border-bottom

## 盒模型属性

### 1. Content区域

```css
.element {
    width: 300px;      /* 内容区域宽度 */
    height: 200px;     /* 内容区域高度 */
    overflow: hidden;  /* 内容溢出处理 */
}
```

### 2. Padding（内边距）

```css
.element {
    /* 四个方向相同 */
    padding: 20px;

    /* 上下、左右 */
    padding: 20px 10px;

    /* 上、左右、下 */
    padding: 20px 10px 15px;

    /* 上、右、下、左 */
    padding: 20px 15px 10px 5px;

    /* 单独设置 */
    padding-top: 20px;
    padding-right: 15px;
    padding-bottom: 10px;
    padding-left: 5px;
}
```

### 3. Border（边框）

```css
.element {
    /* 简写属性 */
    border: 1px solid #000;

    /* 分开设置 */
    border-width: 1px;
    border-style: solid;
    border-color: #000;

    /* 单边设置 */
    border-top: 1px solid #000;
    border-right: 2px dashed #666;
    border-bottom: 3px dotted #999;
    border-left: 4px double #333;

    /* 圆角 */
    border-radius: 5px;
    border-radius: 10px 5px;  /* 左上右下、右上左下 */
    border-radius: 10px 5px 8px 12px;  /* 左上、右上、右下、左下 */
}
```

### 4. Margin（外边距）

```css
.element {
    /* 四个方向相同 */
    margin: 20px;

    /* 上下、左右 */
    margin: 20px auto;  /* 水平居中 */

    /* 上、左右、下 */
    margin: 20px auto 15px;

    /* 上、右、下、左 */
    margin: 20px 15px 10px 5px;

    /* 单独设置 */
    margin-top: 20px;
    margin-right: 15px;
    margin-bottom: 10px;
    margin-left: 5px;
}
```

## 特殊情况

### 1. 外边距合并

垂直方向的外边距会发生合并：

```css
.element1 {
    margin-bottom: 20px;
}

.element2 {
    margin-top: 30px;
}

/* 两个元素之间的实际间距是30px（取较大值）而不是50px */
```

### 2. 百分比值

```css
.element {
    /* 相对于父元素宽度的百分比 */
    width: 50%;
    padding: 10%;
    margin: 5%;
}
```

### 3. 负外边距

```css
.element {
    /* 使用负外边距可以创建特殊的布局效果 */
    margin-top: -20px;
    margin-left: -10px;
}
```

## 实践应用

### 1. 居中布局

```css
/* 水平居中块级元素 */
.center-block {
    width: 200px;
    margin: 0 auto;
}

/* 垂直居中内容 */
.center-content {
    height: 100px;
    line-height: 100px;  /* 单行文本垂直居中 */
    text-align: center;  /* 水平居中 */
}
```

### 2. 清除默认边距

```css
/* 重置默认边距 */
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;  /* 使用IE盒模型 */
}
```

### 3. 响应式布局

```css
.responsive-element {
    width: 90%;           /* 相对宽度 */
    max-width: 1200px;    /* 最大宽度 */
    margin: 0 auto;       /* 水平居中 */
    padding: 20px 5%;     /* 混合使用固定值和百分比 */
}
```

## 最佳实践

### 1. 使用border-box

```css
/* 全局应用border-box */
html {
    box-sizing: border-box;
}

*, *:before, *:after {
    box-sizing: inherit;
}
```

### 2. 避免外边距合并

```css
/* 使用padding代替margin */
.container {
    padding-top: 20px;
    padding-bottom: 20px;
}

/* 或使用overflow创建BFC */
.wrapper {
    overflow: hidden;
}
```

### 3. 响应式设计

```css
.flexible-box {
    width: 100%;
    max-width: 600px;
    padding: 20px;
    margin: 0 auto;
    box-sizing: border-box;
}

@media (max-width: 768px) {
    .flexible-box {
        padding: 10px;
    }
}
```

## 总结

掌握CSS盒模型可以：
- 准确控制元素尺寸和间距
- 创建一致的布局效果
- 避免常见的布局问题
- 实现响应式设计
