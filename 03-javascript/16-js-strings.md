---
title: "JavaScript字符串"
slug: "javascript-strings"
sequence: 16
description: "详细介绍JavaScript字符串的基础知识和使用方法"
is_published: true
estimated_minutes: 25
language: "zh-CN"
---

# JavaScript字符串

## 字符串基础

### 1. 字符串创建

```javascript
// 字符串字面量
const str1 = 'Hello';
const str2 = "World";
const str3 = `Hello World`;  // 模板字符串

// String构造函数
const str4 = new String('Hello');  // 不推荐使用

// 转义字符
const str5 = 'He said: \'Hello\'';
const str6 = "First line\nSecond line";
```

### 2. 字符串属性

```javascript
const str = 'Hello World';

// 字符串长度
console.log(str.length);  // 11

// 访问字符
console.log(str[0]);      // "H"
console.log(str.charAt(0)); // "H"

// Unicode编码
console.log(str.charCodeAt(0));  // 72 (H的Unicode值)
console.log(String.fromCharCode(72));  // "H"
```

## 字符串操作

### 1. 字符串拼接

```javascript
// 使用+运算符
const firstName = '张';
const lastName = '三';
const fullName = firstName + lastName;  // "张三"

// 使用模板字符串
const age = 25;
const message = `${firstName}${lastName}今年${age}岁`;

// concat方法
const greeting = 'Hello'.concat(' ', 'World');  // "Hello World"

// join方法
const words = ['Hello', 'World'];
const sentence = words.join(' ');  // "Hello World"
```

### 2. 字符串修改

```javascript
const str = 'Hello World';

// 转换大小写
console.log(str.toLowerCase());  // "hello world"
console.log(str.toUpperCase());  // "HELLO WORLD"

// 去除空白
const text = '  Hello World  ';
console.log(text.trim());       // "Hello World"
console.log(text.trimStart());  // "Hello World  "
console.log(text.trimEnd());    // "  Hello World"

// 填充字符串
const num = '5';
console.log(num.padStart(3, '0'));  // "005"
console.log(num.padEnd(3, '0'));    // "500"

// 重复字符串
const star = '*';
console.log(star.repeat(5));  // "*****"
```

## 字符串截取

### 1. 提取子串

```javascript
const str = 'Hello World';

// slice方法
console.log(str.slice(0, 5));    // "Hello"
console.log(str.slice(-5));      // "World"

// substring方法
console.log(str.substring(6));    // "World"
console.log(str.substring(0, 5)); // "Hello"

// substr方法（不推荐使用）
console.log(str.substr(6, 5));    // "World"
```

### 2. 分割字符串

```javascript
const sentence = 'The quick brown fox';

// split方法
console.log(sentence.split(' '));     // ["The", "quick", "brown", "fox"]
console.log(sentence.split(''));      // ["T", "h", "e", ...]
console.log(sentence.split(' ', 2));  // ["The", "quick"]

// 实际应用
const csvData = 'name,age,city';
const fields = csvData.split(',');  // ["name", "age", "city"]
```

## 字符串查找

### 1. 位置查找

```javascript
const str = 'Hello World';

// indexOf
console.log(str.indexOf('o'));     // 4
console.log(str.lastIndexOf('o')); // 7

// 查找子字符串
console.log(str.indexOf('World'));  // 6
console.log(str.indexOf('world'));  // -1 (区分大小写)

// includes方法
console.log(str.includes('Hello')); // true
console.log(str.includes('hello')); // false

// startsWith和endsWith
console.log(str.startsWith('Hello')); // true
console.log(str.endsWith('World'));   // true
```

### 2. 正则表达式

```javascript
const text = 'The year is 2025';

// match方法
const numbers = text.match(/\d+/);  // ["2025"]

// matchAll方法
const str = 'cat, bat, sat, fat';
const regex = /[cb]at/g;
const matches = [...str.matchAll(regex)];  // [["cat"], ["bat"]]

// replace方法
const newText = text.replace(/\d+/, '2024');  // "The year is 2024"

// replaceAll方法
const fixed = 'hello hello'.replaceAll('hello', 'hi');  // "hi hi"
```

## 字符串转换

### 1. 类型转换

```javascript
// 转换为字符串
const num = 123;
const str1 = String(num);        // "123"
const str2 = num.toString();     // "123"
const str3 = num + '';          // "123"

// 转换为数字
const str = '123';
const num1 = Number(str);       // 123
const num2 = parseInt(str);     // 123
const num3 = parseFloat('123.45'); // 123.45

// 进制转换
const hex = (255).toString(16);  // "ff"
const binary = (8).toString(2);  // "1000"
```

### 2. 编码转换

```javascript
// URL编码
const url = 'https://example.com/?name=张三';
const encoded = encodeURIComponent(url);
const decoded = decodeURIComponent(encoded);

// Base64编码
const text = 'Hello, World!';
const base64 = btoa(unescape(encodeURIComponent(text)));
const decoded = decodeURIComponent(escape(atob(base64)));

// HTML实体编码
function escapeHTML(str) {
    return str
        .replace(/&/g, '&amp;')
        .replace(/</g, '&lt;')
        .replace(/>/g, '&gt;')
        .replace(/"/g, '&quot;')
        .replace(/'/g, '&#039;');
}
```

## 字符串模板

### 1. 模板字符串

```javascript
// 基本用法
const name = '张三';
const age = 25;
const message = `我叫${name}，今年${age}岁`;

// 多行字符串
const html = `
    <div>
        <h1>标题</h1>
        <p>段落</p>
    </div>
`;

// 表达式计算
const price = 100;
const tax = 0.2;
const total = `总价：${price * (1 + tax)}`;
```

### 2. 标签模板

```javascript
// 自定义标签函数
function highlight(strings, ...values) {
    let result = '';
    strings.forEach((str, i) => {
        result += str;
        if (i < values.length) {
            result += `<span class="highlight">${values[i]}</span>`;
        }
    });
    return result;
}

const name = '张三';
const age = 25;
const html = highlight`我叫${name}，今年${age}岁`;
```

## 实践示例

### 1. 字符串格式化

```javascript
// 数字格式化
function formatNumber(num) {
    return num.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ',');
}

// 日期格式化
function formatDate(date) {
    const options = {
        year: 'numeric',
        month: '2-digit',
        day: '2-digit'
    };
    return new Date(date).toLocaleDateString('zh-CN', options);
}

// 金额格式化
function formatCurrency(amount) {
    return new Intl.NumberFormat('zh-CN', {
        style: 'currency',
        currency: 'CNY'
    }).format(amount);
}
```

### 2. 字符串验证

```javascript
// 邮箱验证
function isValidEmail(email) {
    return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email);
}

// 手机号验证
function isValidPhone(phone) {
    return /^1[3-9]\d{9}$/.test(phone);
}

// 密码强度验证
function checkPasswordStrength(password) {
    const hasLetter = /[a-zA-Z]/.test(password);
    const hasNumber = /\d/.test(password);
    const hasSpecial = /[!@#$%^&*]/.test(password);
    const isLongEnough = password.length >= 8;
    
    return {
        strong: hasLetter && hasNumber && hasSpecial && isLongEnough,
        hasLetter,
        hasNumber,
        hasSpecial,
        isLongEnough
    };
}
```

## 最佳实践

1. 字符串创建
   ```javascript
   // 推荐
   const str = 'Hello';
   const template = `Hello ${name}`;
   
   // 不推荐
   const str = new String('Hello');
   ```

2. 字符串连接
   ```javascript
   // 推荐
   const message = `Hello ${name}`;
   
   // 不推荐
   const message = 'Hello ' + name;
   ```

3. 性能优化
   ```javascript
   // 推荐：使用数组join
   const items = [];
   for (let i = 0; i < 1000; i++) {
       items.push(`item ${i}`);
   }
   const result = items.join('');
   
   // 不推荐：使用+=
   let result = '';
   for (let i = 0; i < 1000; i++) {
       result += `item ${i}`;
   }
   ```

## 总结

- 掌握字符串基础
- 熟练字符串操作
- 使用字符串方法
- 处理字符串转换
- 应用字符串模板
- 遵循最佳实践

下一章将介绍JavaScript字符串方法。
