---
title: "HTML图片"
slug: "html-image"
sequence: 13
description: "学习HTML图片元素的使用，掌握网页图片处理的核心技术"
is_published: true
estimated_minutes: 30
language: "zh-CN"
---

# HTML图片

![HTML图片](./images/html-image.png)
*使用HTML图片元素丰富网页内容*

## 本节概要

通过本节学习，你将学会：
- 在网页中插入图片
- 设置图片的尺寸和属性
- 使用图片的替代文本
- 处理响应式图片

💡 重点内容：
- img标签的基本用法
- 图片属性的设置
- 响应式图片技术
- 图片优化最佳实践

## 1. HTML图片基础

### 基本语法
```html
<img src="图片路径" alt="替代文本">
```

### 常用属性
```html
<!-- 基本图片 -->
<img src="cat.jpg" 
     alt="一只可爱的猫咪" 
     width="300" 
     height="200">

<!-- 带标题的图片 -->
<img src="dog.jpg" 
     alt="一只忠诚的狗狗" 
     title="这是我的宠物狗">
```

## 2. 图片路径

### 相对路径
```html
<!-- 同级目录 -->
<img src="image.jpg" alt="图片">

<!-- 子目录 -->
<img src="images/photo.jpg" alt="照片">

<!-- 上级目录 -->
<img src="../assets/icon.png" alt="图标">
```

### 绝对路径
```html
<!-- 完整URL -->
<img src="https://example.com/images/photo.jpg" alt="网络图片">

<!-- 根目录路径 -->
<img src="/images/logo.png" alt="网站Logo">
```

## 3. 响应式图片

### 使用srcset属性
```html
<img srcset="small.jpg 300w,
             medium.jpg 600w,
             large.jpg 900w"
     sizes="(max-width: 500px) 300px,
            (max-width: 900px) 600px,
            900px"
     src="large.jpg"
     alt="响应式图片">
```

### 使用picture元素
```html
<picture>
    <source media="(min-width: 900px)" srcset="large.jpg">
    <source media="(min-width: 600px)" srcset="medium.jpg">
    <img src="small.jpg" alt="响应式图片">
</picture>
```

## 4. 图片样式

### 基本样式
```css
.responsive-image {
    max-width: 100%;
    height: auto;
    display: block;
    margin: 0 auto;
}
```

### 图片效果
```css
.image-effects {
    /* 圆角 */
    border-radius: 8px;
    
    /* 阴影 */
    box-shadow: 0 4px 8px rgba(0,0,0,0.1);
    
    /* 过渡效果 */
    transition: transform 0.3s ease;
}

.image-effects:hover {
    transform: scale(1.05);
}
```

## 5. 图片优化

### 图片格式选择
- JPEG：适用于照片和复杂图像
- PNG：适用于需要透明度的图像
- WebP：现代高效的图片格式
- SVG：适用于图标和矢量图形

### 性能优化
```html
<!-- 懒加载 -->
<img src="image.jpg" 
     alt="延迟加载图片" 
     loading="lazy">

<!-- 预加载重要图片 -->
<link rel="preload" 
      href="hero.jpg" 
      as="image">
```

## 6. 常见用例

### 图片链接
```html
<a href="page.html">
    <img src="button.png" alt="点击进入">
</a>
```

### 图片地图
```html
<img src="workplace.jpg" alt="工作区" usemap="#workmap">

<map name="workmap">
    <area shape="rect" 
          coords="34,44,270,350" 
          alt="电脑"
          href="computer.html">
    <area shape="rect" 
          coords="290,172,333,250" 
          alt="电话"
          href="phone.html">
</map>
```

## 练习
1. 创建一个响应式图片画廊
2. 实现图片懒加载
3. 优化图片加载性能

## 最佳实践
- 始终设置适当的alt属性
- 使用适合的图片格式
- 优化图片大小和质量
- 实现响应式图片
- 考虑使用懒加载
- 提供适当的图片尺寸

## 扩展阅读
- [MDN Web Docs - Images in HTML](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/img)
- [Web.dev - Images](https://web.dev/images)
- [图片优化指南](https://images.guide/)