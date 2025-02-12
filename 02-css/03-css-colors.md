---
title: "CSS颜色与背景"
slug: "css-colors"
sequence: 3
description: "掌握CSS颜色的表示方法和背景属性的使用"
is_published: true
estimated_minutes: 30
language: "zh-CN"
---

# CSS 颜色与背景

## 颜色值的表示方法

### 1. 颜色关键字

CSS提供了大量预定义的颜色关键字：

```css
.element {
    color: red;
    background-color: black;
    border-color: white;
}
```

常用颜色关键字：
- `black`: 黑色
- `white`: 白色
- `red`: 红色
- `green`: 绿色
- `blue`: 蓝色
- `yellow`: 黄色
- `gray`: 灰色

### 2. RGB 和 RGBA

使用RGB值定义颜色：

```css
/* RGB使用0-255的数值 */
.element {
    color: rgb(255, 0, 0);            /* 红色 */
    background-color: rgb(0, 255, 0);  /* 绿色 */
}

/* RGBA增加了透明度通道（0-1） */
.element {
    background-color: rgba(0, 0, 255, 0.5);  /* 半透明蓝色 */
}
```

### 3. 十六进制颜色码

使用十六进制表示颜色：

```css
.element {
    color: #FF0000;            /* 红色 */
    background-color: #00FF00;  /* 绿色 */
    border-color: #0000FF;     /* 蓝色 */
}

/* 简写形式（当每种颜色都重复时） */
.element {
    color: #F00;  /* 等同于 #FF0000 */
}
```

### 4. HSL 和 HSLA

使用色相、饱和度、亮度定义颜色：

```css
/* HSL: 色相(0-360)、饱和度(0%-100%)、亮度(0%-100%) */
.element {
    color: hsl(0, 100%, 50%);          /* 红色 */
    background-color: hsl(120, 100%, 50%);  /* 绿色 */
}

/* HSLA增加透明度通道 */
.element {
    background-color: hsla(240, 100%, 50%, 0.5);  /* 半透明蓝色 */
}
```

## 背景属性

### 1. background-color

设置元素的背景颜色：

```css
.element {
    background-color: #f0f0f0;
    background-color: rgba(240, 240, 240, 0.8);
}
```

### 2. background-image

设置背景图片：

```css
.element {
    background-image: url('image.jpg');
    
    /* 可以设置多个背景图片 */
    background-image: url('top.png'), url('bottom.png');
}
```

### 3. background-repeat

控制背景图片的重复方式：

```css
.element {
    background-repeat: no-repeat;  /* 不重复 */
    background-repeat: repeat-x;   /* 水平重复 */
    background-repeat: repeat-y;   /* 垂直重复 */
    background-repeat: repeat;     /* 双向重复 */
}
```

### 4. background-position

设置背景图片的位置：

```css
.element {
    /* 使用关键字 */
    background-position: center center;
    background-position: top left;
    
    /* 使用具体数值 */
    background-position: 50% 50%;
    background-position: 20px 30px;
}
```

### 5. background-size

控制背景图片的大小：

```css
.element {
    background-size: cover;      /* 覆盖整个容器 */
    background-size: contain;    /* 确保图片完全显示 */
    background-size: 100% 100%;  /* 拉伸至指定大小 */
    background-size: 50px auto;  /* 指定宽度，高度自适应 */
}
```

### 6. background 简写属性

组合多个背景属性：

```css
.element {
    background: #f0f0f0 url('image.jpg') no-repeat center center / cover;
}
```

## 渐变背景

### 1. 线性渐变

```css
.element {
    /* 从上到下 */
    background: linear-gradient(red, yellow);
    
    /* 指定角度 */
    background: linear-gradient(45deg, red, yellow);
    
    /* 多个颜色节点 */
    background: linear-gradient(red, yellow, blue);
    
    /* 使用透明度 */
    background: linear-gradient(rgba(255,0,0,0.8), rgba(255,255,0,0.8));
}
```

### 2. 径向渐变

```css
.element {
    /* 基本径向渐变 */
    background: radial-gradient(red, yellow);
    
    /* 指定形状和大小 */
    background: radial-gradient(circle at center, red, yellow);
    
    /* 多个颜色节点 */
    background: radial-gradient(red, yellow, blue);
}
```

## 实践技巧

### 1. 颜色变量

使用CSS变量定义颜色主题：

```css
:root {
    --primary-color: #007bff;
    --secondary-color: #6c757d;
    --success-color: #28a745;
}

.element {
    color: var(--primary-color);
    background-color: var(--secondary-color);
}
```

### 2. 颜色透明度

创建半透明效果：

```css
.overlay {
    /* 使用rgba */
    background-color: rgba(0, 0, 0, 0.5);
    
    /* 或使用opacity */
    background-color: black;
    opacity: 0.5;
}
```

### 3. 配色方案

创建协调的配色方案：

```css
:root {
    /* 主色调 */
    --primary: #007bff;
    --primary-light: #4da3ff;
    --primary-dark: #0056b3;
    
    /* 辅助色 */
    --accent: #ff6b6b;
    
    /* 中性色 */
    --gray-100: #f8f9fa;
    --gray-900: #212529;
}
```

## 总结

掌握CSS颜色和背景属性可以：
- 创建视觉吸引力强的界面
- 提升用户体验
- 建立品牌识别度
- 实现各种视觉效果