---
title: "HTML中的JavaScript"
slug: "html-javascript"
sequence: 22
description: "深入理解在HTML中使用JavaScript的方法、最佳实践和常见应用场景"
is_published: true
estimated_minutes: 30
language: "zh-CN"
---

# HTML中的JavaScript

![HTML中的JavaScript](./images/html-javascript.png)
*在HTML中使用JavaScript增强交互性*

## 本节概要

通过本节学习，你将掌握：
- JavaScript在HTML中的基本用法
- 脚本加载策略
- 常见的DOM操作
- 事件处理机制

💡 重点内容：
- 脚本引入方式
- 加载优化策略
- DOM操作技巧
- 事件处理最佳实践

## 1. JavaScript基础引入

### 内联脚本
```html
<!-- 在HTML中直接编写JavaScript -->
<script>
    // 直接在页面中编写JavaScript代码
    document.addEventListener('DOMContentLoaded', () => {
        console.log('页面加载完成！');
    });
</script>
```

### 外部脚本
```html
<!-- 引入外部JavaScript文件 -->
<script src="main.js"></script>

<!-- 使用现代特性 -->
<script src="module.js" type="module"></script>

<!-- 异步加载脚本 -->
<script src="async-script.js" async></script>

<!-- 延迟加载脚本 -->
<script src="defer-script.js" defer></script>
```

## 2. 脚本加载策略

### 基本加载方式
```html
<!-- 传统方式：放在</body>之前 -->
<body>
    <div id="content">页面内容</div>
    <script src="script.js"></script>
</body>

<!-- 现代方式：使用defer属性 -->
<head>
    <script src="script.js" defer></script>
</head>
```

### 动态加载
```html
<script>
// 动态创建和加载脚本
function loadScript(src) {
    return new Promise((resolve, reject) => {
        const script = document.createElement('script');
        script.src = src;
        script.onload = () => resolve(script);
        script.onerror = () => reject(new Error(`Script load error: ${src}`));
        document.head.appendChild(script);
    });
}

// 使用示例
loadScript('https://example.com/script.js')
    .then(() => console.log('脚本加载成功'))
    .catch(error => console.error('脚本加载失败:', error));
</script>
```

## 3. DOM操作

### 基本选择器
```html
<div id="app">
    <h1 class="title">标题</h1>
    <p class="content">内容</p>
</div>

<script>
// 通过ID选择
const app = document.getElementById('app');

// 通过类名选择
const titles = document.getElementsByClassName('title');

// 使用querySelector
const content = document.querySelector('.content');

// 使用querySelectorAll
const elements = document.querySelectorAll('.content');
</script>
```

### DOM操作示例
```html
<div id="container">
    <button id="addBtn">添加项目</button>
    <ul id="list"></ul>
</div>

<script>
document.getElementById('addBtn').addEventListener('click', () => {
    // 创建新元素
    const li = document.createElement('li');
    li.textContent = `项目 ${Date.now()}`;
    
    // 添加样式
    li.style.color = '#333';
    li.classList.add('list-item');
    
    // 插入DOM
    document.getElementById('list').appendChild(li);
});
</script>

<style>
.list-item {
    padding: 10px;
    margin: 5px 0;
    background: #f5f5f5;
    border-radius: 4px;
}
</style>
```

## 4. 事件处理

### 基本事件绑定
```html
<button onclick="handleClick()">点击我</button>

<button id="myButton">更好的方式</button>

<script>
// 传统方式
function handleClick() {
    alert('按钮被点击！');
}

// 现代方式
document.getElementById('myButton').addEventListener('click', (event) => {
    console.log('事件对象：', event);
    alert('使用addEventListener绑定的事件');
});
</script>
```

### 事件委托
```html
<ul id="taskList">
    <li>任务1</li>
    <li>任务2</li>
    <li>任务3</li>
</ul>

<script>
// 使用事件委托处理列表项点击
document.getElementById('taskList').addEventListener('click', (event) => {
    if (event.target.tagName === 'LI') {
        event.target.classList.toggle('completed');
    }
});
</script>

<style>
.completed {
    text-decoration: line-through;
    color: #999;
}
</style>
```

## 5. 实际应用示例

### 表单验证
```html
<form id="registrationForm">
    <div class="form-group">
        <label for="username">用户名：</label>
        <input type="text" id="username" required>
        <span class="error"></span>
    </div>
    
    <div class="form-group">
        <label for="email">邮箱：</label>
        <input type="email" id="email" required>
        <span class="error"></span>
    </div>
    
    <button type="submit">提交</button>
</form>

<script>
document.getElementById('registrationForm').addEventListener('submit', (event) => {
    event.preventDefault();
    
    const username = document.getElementById('username');
    const email = document.getElementById('email');
    
    // 验证用户名
    if (username.value.length < 3) {
        showError(username, '用户名至少需要3个字符');
        return;
    }
    
    // 验证邮箱
    const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    if (!emailRegex.test(email.value)) {
        showError(email, '请输入有效的邮箱地址');
        return;
    }
    
    // 提交表单
    alert('表单验证通过！');
});

function showError(element, message) {
    const error = element.nextElementSibling;
    error.textContent = message;
    element.classList.add('invalid');
}
</script>

<style>
.form-group {
    margin-bottom: 15px;
}

.error {
    color: red;
    font-size: 12px;
}

.invalid {
    border-color: red;
}
</style>
```

### 动态内容加载
```html
<div id="posts">
    <button id="loadMore">加载更多</button>
</div>

<script>
let page = 1;

document.getElementById('loadMore').addEventListener('click', async () => {
    try {
        const response = await fetch(`/api/posts?page=${page}`);
        const posts = await response.json();
        
        posts.forEach(post => {
            const article = document.createElement('article');
            article.innerHTML = `
                <h2>${post.title}</h2>
                <p>${post.content}</p>
            `;
            document.getElementById('posts').insertBefore(
                article, 
                document.getElementById('loadMore')
            );
        });
        
        page++;
    } catch (error) {
        console.error('加载失败:', error);
    }
});
</script>
```

## 6. 性能优化

### 脚本加载优化
```html
<!-- 关键脚本立即加载 -->
<script src="critical.js"></script>

<!-- 非关键脚本延迟加载 -->
<script src="non-critical.js" defer></script>

<!-- 独立功能异步加载 -->
<script src="independent.js" async></script>

<!-- 模块化加载 -->
<script type="module">
    import { feature } from './module.js';
</script>
```

### 性能最佳实践
```javascript
// 使用节流函数优化滚动事件
function throttle(func, limit) {
    let inThrottle;
    return function(...args) {
        if (!inThrottle) {
            func.apply(this, args);
            inThrottle = true;
            setTimeout(() => inThrottle = false, limit);
        }
    }
}

// 应用节流到滚动事件
window.addEventListener('scroll', throttle(() => {
    console.log('滚动位置：', window.scrollY);
}, 100));

// 使用requestAnimationFrame优化动画
function animate() {
    // 更新动画
    requestAnimationFrame(animate);
}
```

## 7. 调试技巧

### 常用调试方法
```javascript
// 使用console
console.log('普通日志');
console.warn('警告信息');
console.error('错误信息');
console.table([{name: 'John', age: 30}, {name: 'Jane', age: 25}]);

// 使用debugger
function debugFunction() {
    debugger; // 代码会在这里暂停
    // 继续执行的代码
}

// 错误处理
try {
    // 可能出错的代码
    throw new Error('发生错误');
} catch (error) {
    console.error('捕获到错误:', error);
} finally {
    // 清理代码
}
```

## 练习
1. 创建一个带验证的注册表单
2. 实现一个无限滚动的图片列表
3. 开发一个简单的待办事项应用

## 扩展阅读
- [MDN - JavaScript指南](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide)
- [现代JavaScript教程](https://zh.javascript.info/)
- [JavaScript性能优化](https://web.dev/fast/#optimize-your-javascript)
