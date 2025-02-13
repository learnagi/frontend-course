---
title: "JavaScript输出"
slug: "javascript-output"
sequence: 3
description: "了解JavaScript的各种输出方式"
is_published: true
estimated_minutes: 15
language: "zh-CN"
---

# JavaScript输出

## 输出方式

### 1. console对象

```javascript
// 基本输出
console.log("Hello World");        // 普通信息
console.info("提示信息");          // 提示信息
console.warn("警告信息");          // 警告信息
console.error("错误信息");         // 错误信息

// 格式化输出
console.log("姓名：%s，年龄：%d", "张三", 20);

// 表格输出
console.table([
    { name: "张三", age: 20 },
    { name: "李四", age: 25 }
]);

// 分组输出
console.group("用户信息");
console.log("姓名：张三");
console.log("年龄：20");
console.groupEnd();

// 计时功能
console.time("计时器");
// 执行一些操作
console.timeEnd("计时器");
```

### 2. 弹出框

```javascript
// 警告框
alert("警告信息");

// 确认框
if (confirm("确定要删除吗？")) {
    console.log("用户点击了确定");
} else {
    console.log("用户点击了取消");
}

// 输入框
let name = prompt("请输入您的名字", "默认值");
if (name) {
    console.log("您好，" + name);
}
```

### 3. DOM输出

```javascript
// 修改HTML内容
document.getElementById("demo").innerHTML = "新内容";

// 修改HTML属性
document.getElementById("myImage").src = "new.jpg";

// 修改CSS样式
document.getElementById("demo").style.color = "red";

// 创建新元素
let element = document.createElement("p");
element.textContent = "新段落";
document.body.appendChild(element);
```

### 4. document.write()

```javascript
// 基本使用（不推荐）
document.write("<h1>Hello World</h1>");

// 注意：在页面加载完成后使用document.write会覆盖整个页面
window.onload = function() {
    // 不要这样做！
    document.write("这会覆盖整个页面");
};
```

## 调试输出

### 1. 调试工具

```javascript
// 设置断点
debugger;

// 输出调试信息
console.debug("调试信息");

// 输出对象结构
let user = { name: "张三", age: 20 };
console.dir(user);

// 输出调用栈
console.trace("跟踪调用");
```

### 2. 性能分析

```javascript
// 性能分析
console.profile("性能分析");
// 执行一些操作
console.profileEnd("性能分析");

// 计数器
for (let i = 0; i < 3; i++) {
    console.count("循环计数");
}
```

## 实践示例

### 1. 日志工具

```javascript
// 创建简单的日志工具
const Logger = {
    info(message) {
        console.log(`[INFO] ${new Date().toISOString()}: ${message}`);
    },
    
    warn(message) {
        console.warn(`[WARN] ${new Date().toISOString()}: ${message}`);
    },
    
    error(message) {
        console.error(`[ERROR] ${new Date().toISOString()}: ${message}`);
    }
};

// 使用示例
Logger.info("应用启动");
Logger.warn("配置文件未找到");
Logger.error("发生错误");
```

### 2. 动态内容更新

```javascript
// 创建动态内容更新器
class ContentUpdater {
    constructor(elementId) {
        this.element = document.getElementById(elementId);
    }
    
    setText(text) {
        this.element.textContent = text;
    }
    
    setHTML(html) {
        this.element.innerHTML = html;
    }
    
    addClass(className) {
        this.element.classList.add(className);
    }
    
    removeClass(className) {
        this.element.classList.remove(className);
    }
}

// 使用示例
const updater = new ContentUpdater("output");
updater.setText("更新的文本");
updater.addClass("highlight");
```

## 最佳实践

1. 输出选择
   - 开发时使用console.log进行调试
   - 生产环境移除或禁用调试输出
   - 避免使用document.write

2. 性能考虑
   - 避免过多的console输出
   - 合理使用console.table展示数据
   - 使用性能分析工具优化代码

3. 调试技巧
   - 使用断点而不是console.log
   - 利用console.group组织输出
   - 使用自定义的日志工具

## 练习

```javascript
// 1. 创建一个简单的控制台日志系统
class ConsoleLogger {
    static log(type, message) {
        const timestamp = new Date().toISOString();
        const formattedMessage = `[${type.toUpperCase()}] ${timestamp}: ${message}`;
        
        switch (type) {
            case "info":
                console.log(formattedMessage);
                break;
            case "warn":
                console.warn(formattedMessage);
                break;
            case "error":
                console.error(formattedMessage);
                break;
            default:
                console.log(formattedMessage);
        }
    }
}

// 2. 创建一个DOM更新器
class DOMUpdater {
    static update(elementId, content, type = "text") {
        const element = document.getElementById(elementId);
        if (!element) return false;
        
        switch (type) {
            case "text":
                element.textContent = content;
                break;
            case "html":
                element.innerHTML = content;
                break;
            case "value":
                element.value = content;
                break;
        }
        return true;
    }
}
```

## 总结

- 掌握不同的输出方式
- 了解调试工具的使用
- 创建自定义日志工具
- 注意性能和安全性
- 遵循最佳实践

下一章将介绍JavaScript的语句和语法。
