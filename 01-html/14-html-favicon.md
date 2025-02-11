---
title: "HTML网站图标"
slug: "html-favicon"
sequence: 14
description: "学习如何为网站添加favicon图标，提升网站的专业性和品牌识别度"
is_published: true
estimated_minutes: 20
language: "zh-CN"
---

# HTML网站图标（Favicon）

![HTML Favicon](./images/html-favicon.png)
*为网站添加专属图标，提升品牌识别度*

## 本节概要

通过本节学习，你将学会：
- 理解favicon的作用和重要性
- 创建适合的favicon图标
- 在HTML中正确引用favicon
- 为不同设备优化favicon

💡 重点内容：
- Favicon的基本概念
- 图标格式和尺寸
- 引用方法和兼容性
- 最佳实践建议

## 1. Favicon基础

### 什么是Favicon
Favicon（Favorites Icon）是显示在浏览器标签页、书签栏和其他位置的小图标，用于标识特定的网站。

### 基本用法
```html
<!-- 基本favicon -->
<link rel="icon" href="favicon.ico">

<!-- 指定类型的favicon -->
<link rel="icon" type="image/png" href="favicon.png">
```

## 2. 支持的格式

### 常用格式
```html
<!-- ICO格式（传统格式，兼容性最好） -->
<link rel="icon" href="favicon.ico">

<!-- PNG格式（支持透明度） -->
<link rel="icon" type="image/png" href="favicon.png">

<!-- SVG格式（矢量图，可缩放） -->
<link rel="icon" type="image/svg+xml" href="favicon.svg">
```

### 不同尺寸
```html
<!-- 16x16像素（标准尺寸） -->
<link rel="icon" type="image/png" sizes="16x16" href="favicon-16x16.png">

<!-- 32x32像素（高DPI显示器） -->
<link rel="icon" type="image/png" sizes="32x32" href="favicon-32x32.png">

<!-- 96x96像素（Windows Metro） -->
<link rel="icon" type="image/png" sizes="96x96" href="favicon-96x96.png">
```

## 3. 移动设备支持

### iOS设备
```html
<!-- iPhone -->
<link rel="apple-touch-icon" sizes="180x180" href="apple-touch-icon.png">
<link rel="apple-touch-icon" sizes="120x120" href="apple-touch-icon-120x120.png">
<link rel="apple-touch-icon" sizes="76x76" href="apple-touch-icon-76x76.png">
```

### Android设备
```html
<!-- Android Chrome -->
<link rel="manifest" href="site.webmanifest">
<meta name="theme-color" content="#ffffff">
```

## 4. 完整示例

### 基础HTML设置
```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <!-- 标准favicon -->
    <link rel="icon" href="favicon.ico">
    
    <!-- 现代浏览器 -->
    <link rel="icon" type="image/png" sizes="32x32" href="favicon-32x32.png">
    <link rel="icon" type="image/png" sizes="16x16" href="favicon-16x16.png">
    
    <!-- iOS设备 -->
    <link rel="apple-touch-icon" sizes="180x180" href="apple-touch-icon.png">
    
    <!-- Android设备 -->
    <link rel="manifest" href="site.webmanifest">
    <meta name="theme-color" content="#ffffff">
    
    <title>我的网站</title>
</head>
<body>
    <!-- 网站内容 -->
</body>
</html>
```

### Web应用清单（site.webmanifest）
```json
{
    "name": "网站名称",
    "short_name": "短名称",
    "icons": [
        {
            "src": "android-chrome-192x192.png",
            "sizes": "192x192",
            "type": "image/png"
        },
        {
            "src": "android-chrome-512x512.png",
            "sizes": "512x512",
            "type": "image/png"
        }
    ],
    "theme_color": "#ffffff",
    "background_color": "#ffffff",
    "display": "standalone"
}
```

## 5. 创建Favicon

### 推荐工具
1. [Favicon Generator](https://realfavicongenerator.net/)
   - 上传一张高质量图片
   - 自动生成各种尺寸
   - 提供完整的HTML代码

2. [Favicon.io](https://favicon.io/)
   - 支持从文本创建
   - 支持从图片创建
   - 支持从emoji创建

## 6. 最佳实践

### 设计建议
- 使用简单、清晰的设计
- 确保在小尺寸下仍可识别
- 与品牌标识保持一致
- 考虑深色/浅色模式

### 技术建议
- 提供多种尺寸的图标
- 使用适当的图片格式
- 确保文件大小优化
- 定期检查图标是否正常显示

### 性能优化
```html
<!-- 预加载关键图标 -->
<link rel="preload" href="favicon.ico" as="image">
```

## 练习
1. 为你的网站创建一个基本的favicon
2. 生成并添加不同尺寸的图标
3. 测试在不同设备上的显示效果

## 常见问题
- 图标不显示
  - 检查文件路径是否正确
  - 确认文件格式是否支持
  - 清除浏览器缓存

- 图标模糊
  - 提供更高分辨率的版本
  - 使用SVG格式
  - 确保原始图片质量

## 扩展阅读
- [MDN Web Docs - Favicon](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/link#attr-sizes)
- [HTML5 Favicon](https://css-tricks.com/favicon-quiz/)
- [Web App Manifest](https://developer.mozilla.org/zh-CN/docs/Web/Manifest)