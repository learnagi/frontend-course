---
title: "JavaScript语句和语法"
slug: "javascript-statements-syntax"
sequence: 4
description: "了解JavaScript的基本语句和语法规则"
is_published: true
estimated_minutes: 20
language: "zh-CN"
---

# JavaScript语句和语法

## 基本语法规则

### 1. 语句和分号

```javascript
// 语句以分号结束（可选但推荐）
let name = "张三";
console.log(name);

// 一行多个语句
let a = 5; let b = 6; let c = a + b;

// 语句可以跨多行
let longString = "这是一个很长的字符串" + 
                "需要跨多行显示" + 
                "以提高可读性";
```

### 2. 大小写敏感

```javascript
// JavaScript区分大小写
let color = "red";
let Color = "blue";
let COLOR = "green";

// 这些是三个不同的变量
console.log(color);  // "red"
console.log(Color);  // "blue"
console.log(COLOR);  // "green"
```

### 3. 空格和换行

```javascript
// 空格和换行通常被忽略
let x=1;
let y    =    2;
let z=
3;

// 但要注意某些情况
let a = 1 + 2;      // 正确
let b = 1+2;        // 正确但不推荐
let c = 1 +         // 正确
        2;
```

## 代码块

### 1. 块级作用域

```javascript
// 使用花括号定义代码块
{
    let blockScoped = "只在块内可见";
    const PI = 3.14159;
    
    console.log(blockScoped); // 正常工作
}
// console.log(blockScoped); // 错误：blockScoped未定义

// if语句中的代码块
if (true) {
    let message = "条件为真";
    console.log(message);
}

// 函数中的代码块
function example() {
    let local = "局部变量";
    return local;
}
```

### 2. 缩进和格式

```javascript
// 推荐的缩进风格
function calculate(a, b) {
    let result;
    if (a > b) {
        result = a - b;
    } else {
        result = a + b;
    }
    return result;
}

// 不推荐的缩进风格
function badExample(a,b)
{
result = a+b;
if(result>0){
console.log(result);
}
return result;
}
```

## 注释

### 1. 单行注释

```javascript
// 这是单行注释
let x = 5; // 这也是单行注释

// 多个单行注释
// 作者：张三
// 日期：2024-02-13
// 描述：示例代码
```

### 2. 多行注释

```javascript
/* 这是一个
   多行注释
   可以跨越多行 */

/* 
 * 这是一种更有组织的
 * 多行注释格式
 * 每行都以星号开头
 */

/**
 * 这是JSDoc风格的文档注释
 * @param {string} name - 用户名
 * @returns {string} 格式化的问候语
 */
function greet(name) {
    return `Hello, ${name}!`;
}
```

## 标识符

### 1. 命名规则

```javascript
// 有效的标识符
let name = "张三";
let _private = "私有变量";
let $element = document.getElementById("main");
let firstName = "John";
let lastName123 = "Doe";

// 无效的标识符
// let 123name = "错误";    // 不能以数字开头
// let my-name = "错误";    // 不能包含连字符
// let new = "错误";        // 不能使用关键字
```

### 2. 命名约定

```javascript
// 驼峰命名法（推荐）
let firstName = "John";
let lastName = "Doe";
let isStudent = true;

// 构造函数使用大驼峰
class Person {
    constructor(name) {
        this.name = name;
    }
}

// 常量使用大写字母和下划线
const MAX_SIZE = 100;
const API_KEY = "abc123";

// 私有变量前缀使用下划线
class Example {
    constructor() {
        this._privateVar = "私有";
    }
}
```

## 关键字和保留字

```javascript
// 常见关键字
let myVar;      // let - 声明变量
const PI = 3.14; // const - 声明常量
if (true) {}    // if - 条件语句
for (;;) {}     // for - 循环语句
while (true) {} // while - 循环语句
function fn() {} // function - 函数声明
return;         // return - 返回语句
break;          // break - 跳出循环
continue;       // continue - 继续循环

// 不能用作标识符的保留字
// class, enum, extends, super, const, export, import
```

## 最佳实践

1. 代码格式
   - 使用一致的缩进（2或4个空格）
   - 适当使用空行分隔代码块
   - 运算符周围添加空格
   - 使用分号结束语句

2. 命名规范
   - 使用有意义的名称
   - 遵循驼峰命名法
   - 常量使用大写字母
   - 避免使用单字母变量名（除非是循环计数器）

3. 注释规范
   - 及时更新注释
   - 使用JSDoc记录函数
   - 避免无意义的注释
   - 代码即文档，写出自解释的代码

## 练习

```javascript
// 1. 格式化代码示例
function calculateArea(width, height) {
    // 验证输入
    if (typeof width !== "number" || typeof height !== "number") {
        throw new TypeError("参数必须是数字");
    }
    
    // 计算面积
    const area = width * height;
    
    // 返回结果，保留两位小数
    return Number(area.toFixed(2));
}

// 2. 命名规范示例
class BankAccount {
    constructor(initialBalance) {
        this._balance = initialBalance;
        this.MINIMUM_BALANCE = 0;
        this.MAXIMUM_WITHDRAWAL = 10000;
    }
    
    getBalance() {
        return this._balance;
    }
    
    withdraw(amount) {
        if (this._balance - amount >= this.MINIMUM_BALANCE) {
            this._balance -= amount;
            return true;
        }
        return false;
    }
}
```

## 总结

- 理解基本语法规则
- 遵循代码格式规范
- 使用合适的命名约定
- 正确使用注释
- 避免使用保留字
- 保持代码整洁和可读性

下一章将介绍JavaScript的变量声明和使用。
