---
title: "JavaScript在哪里"
slug: "javascript-where-to"
sequence: 2
description: "了解如何在HTML中使用JavaScript"
is_published: true
estimated_minutes: 15
language: "zh-CN"
---

# JavaScript在哪里使用

## HTML中的JavaScript

### 1. 内部JavaScript

```html
<!DOCTYPE html>
<html>
<head>
    <title>内部JavaScript</title>
    <script>
        function sayHello() {
            alert("Hello World!");
        }
    </script>
</head>
<body>
    <button onclick="sayHello()">点击我</button>
</body>
</html>
```

### 2. 外部JavaScript

```html
<!DOCTYPE html>
<html>
<head>
    <title>外部JavaScript</title>
    <!-- 在head中引入JavaScript -->
    <script src="script.js"></script>
</head>
<body>
    <h1>我的网页</h1>
    
    <!-- 在body末尾引入JavaScript（推荐） -->
    <script src="app.js"></script>
</body>
</html>
```

### 3. 内联JavaScript

```html
<!-- 不推荐使用内联JavaScript -->
<button onclick="alert('Hello!')">点击</button>
```

## JavaScript放置位置

### 1. 头部引入

```html
<!DOCTYPE html>
<html>
<head>
    <script src="script1.js"></script>
    <script src="script2.js"></script>
</head>
<body>
    <!-- 页面内容 -->
</body>
</html>
```

### 2. 底部引入（推荐）

```html
<!DOCTYPE html>
<html>
<head>
    <title>我的网页</title>
</head>
<body>
    <!-- 页面内容 -->
    
    <!-- 在body结束标签前引入JavaScript -->
    <script src="script1.js"></script>
    <script src="script2.js"></script>
</body>
</html>
```

## 加载策略

### 1. 默认加载

```html
<script src="script.js"></script>
```

### 2. 异步加载（async）

```html
<!-- 异步下载，下载完立即执行 -->
<script async src="script.js"></script>
```

### 3. 延迟加载（defer）

```html
<!-- 异步下载，等待HTML解析完成后执行 -->
<script defer src="script.js"></script>
```

## 模块化JavaScript

### 1. 使用模块

```html
<script type="module" src="main.js"></script>
```

```javascript
// main.js
import { sayHello } from './greet.js';

sayHello('World');
```

```javascript
// greet.js
export function sayHello(name) {
    console.log(`Hello, ${name}!`);
}
```

## 最佳实践

1. 脚本位置
   - 将脚本放在body结束标签前
   - 使用defer属性进行延迟加载
   - 避免使用内联JavaScript

2. 性能优化
   - 合并多个JavaScript文件
   - 使用async加载非关键脚本
   - 压缩JavaScript文件

3. 可维护性
   - 使用外部JavaScript文件
   - 采用模块化开发
   - 保持代码结构清晰

## 常见问题

### 1. 加载顺序

```html
<!-- 按顺序加载和执行 -->
<script src="jquery.js"></script>
<script src="app.js"></script>

<!-- 使用defer保持顺序 -->
<script defer src="jquery.js"></script>
<script defer src="app.js"></script>

<!-- async不保证顺序 -->
<script async src="script1.js"></script>
<script async src="script2.js"></script>
```

### 2. 跨域问题

```html
<!-- 处理跨域 -->
<script src="https://example.com/script.js" crossorigin="anonymous"></script>
```

## 总结

- 了解JavaScript在HTML中的不同使用方式
- 掌握脚本加载策略
- 遵循最佳实践
- 注意性能优化
- 处理常见问题

下一章将介绍JavaScript的输出方式。
