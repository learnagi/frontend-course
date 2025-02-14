---
title: "JavaScript字符串方法"
slug: "javascript-string-methods"
sequence: 17
description: "详细介绍JavaScript字符串的各种方法及其使用"
is_published: true
estimated_minutes: 25
language: "zh-CN"
---

# JavaScript字符串方法

## 基本方法

### 1. 长度和访问

```javascript
const str = 'Hello World';

// 获取长度
console.log(str.length);  // 11

// 访问字符
console.log(str.charAt(0));     // "H"
console.log(str.charCodeAt(0)); // 72
console.log(str[0]);           // "H"

// 获取Unicode码点
console.log(str.codePointAt(0)); // 72
```

### 2. 大小写转换

```javascript
const text = 'Hello World';

// 转换为大写
console.log(text.toUpperCase());  // "HELLO WORLD"

// 转换为小写
console.log(text.toLowerCase());  // "hello world"

// 本地化转换
console.log(text.toLocaleLowerCase());
console.log(text.toLocaleUpperCase());
```

## 查找方法

### 1. 位置查找

```javascript
const str = 'Hello World, Hello JavaScript';

// indexOf
console.log(str.indexOf('Hello'));     // 0
console.log(str.indexOf('Hello', 1));  // 13 (从索引1开始查找)

// lastIndexOf
console.log(str.lastIndexOf('Hello')); // 13
console.log(str.lastIndexOf('o'));     // 19

// search（支持正则表达式）
console.log(str.search(/World/));      // 6
console.log(str.search(/world/i));     // 6 (忽略大小写)
```

### 2. 包含检查

```javascript
const str = 'Hello World';

// includes
console.log(str.includes('Hello'));     // true
console.log(str.includes('hello'));     // false

// startsWith
console.log(str.startsWith('Hello'));   // true
console.log(str.startsWith('World', 6)); // true (从索引6开始检查)

// endsWith
console.log(str.endsWith('World'));     // true
console.log(str.endsWith('Hello', 5));  // true (检查前5个字符)
```

## 提取方法

### 1. 截取字符串

```javascript
const str = 'Hello World';

// slice
console.log(str.slice(0, 5));    // "Hello"
console.log(str.slice(-5));      // "World"
console.log(str.slice(6));       // "World"

// substring
console.log(str.substring(0, 5)); // "Hello"
console.log(str.substring(6));    // "World"

// substr（不推荐使用）
console.log(str.substr(6, 5));    // "World"
```

### 2. 分割字符串

```javascript
const str = 'apple,banana,orange';

// split
console.log(str.split(','));     // ["apple", "banana", "orange"]
console.log(str.split(''));      // ["a", "p", "p", "l", "e", ...]
console.log(str.split(',', 2));  // ["apple", "banana"]

// 实际应用
const date = '2025-02-14';
const [year, month, day] = date.split('-');
```

## 修改方法

### 1. 替换内容

```javascript
const str = 'Hello World';

// replace
console.log(str.replace('World', 'JavaScript')); 
// "Hello JavaScript"

// replaceAll
const text = 'cat cat cat';
console.log(text.replaceAll('cat', 'dog')); 
// "dog dog dog"

// 使用正则表达式
const html = '<div>Hello</div>';
console.log(html.replace(/<[^>]+>/g, '')); 
// "Hello"
```

### 2. 填充和修剪

```javascript
// padStart和padEnd
const num = '5';
console.log(num.padStart(3, '0'));  // "005"
console.log(num.padEnd(3, '0'));    // "500"

// trim方法
const text = '  Hello World  ';
console.log(text.trim());           // "Hello World"
console.log(text.trimStart());      // "Hello World  "
console.log(text.trimEnd());        // "  Hello World"

// repeat方法
const star = '*';
console.log(star.repeat(5));        // "*****"
```

## 正则表达式方法

### 1. 匹配方法

```javascript
const text = 'The year is 2025';

// match
const numbers = text.match(/\d+/);
console.log(numbers[0]);  // "2025"

// matchAll
const str = 'cat, bat, sat, fat';
const regex = /[cb]at/g;
for (const match of str.matchAll(regex)) {
    console.log(match[0]);  // "cat", "bat"
}

// 命名捕获组
const date = '2025-02-14';
const dateRegex = /(?<year>\d{4})-(?<month>\d{2})-(?<day>\d{2})/;
const groups = date.match(dateRegex).groups;
console.log(groups.year);  // "2025"
```

### 2. 测试方法

```javascript
// test方法（在RegExp原型上）
const email = 'test@example.com';
const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
console.log(emailRegex.test(email));  // true

// 常用正则表达式模式
const patterns = {
    email: /^[^\s@]+@[^\s@]+\.[^\s@]+$/,
    phone: /^1[3-9]\d{9}$/,
    url: /^(https?:\/\/)?([\da-z.-]+)\.([a-z.]{2,6})([\/\w .-]*)*\/?$/
};
```

## 转换方法

### 1. 字符串转换

```javascript
// toString方法
const num = 123;
console.log(num.toString());     // "123"
console.log(num.toString(2));    // "1111011" (二进制)
console.log(num.toString(16));   // "7b" (十六进制)

// String方法
console.log(String(null));       // "null"
console.log(String(undefined));  // "undefined"
console.log(String(true));       // "true"
```

### 2. 编码转换

```javascript
// 字符编码
const text = 'Hello';
console.log(text.charCodeAt(0));         // 72
console.log(String.fromCharCode(72));    // "H"

// Unicode编码
console.log(text.codePointAt(0));        // 72
console.log(String.fromCodePoint(72));   // "H"

// Base64编码
const str = 'Hello World';
const encoded = btoa(unescape(encodeURIComponent(str)));
const decoded = decodeURIComponent(escape(atob(encoded)));
```

## 实践示例

### 1. 字符串处理工具

```javascript
class StringUtils {
    // 首字母大写
    static capitalize(str) {
        return str.charAt(0).toUpperCase() + str.slice(1);
    }
    
    // 驼峰命名转换
    static toCamelCase(str) {
        return str.toLowerCase()
            .replace(/[_-\s]([a-z])/g, (_, char) => char.toUpperCase());
    }
    
    // 截断字符串
    static truncate(str, length, ending = '...') {
        if (str.length <= length) return str;
        return str.slice(0, length - ending.length) + ending;
    }
    
    // 格式化字符串
    static format(str, ...args) {
        return str.replace(/{(\d+)}/g, (match, index) => {
            return args[index] !== undefined ? args[index] : match;
        });
    }
}

// 使用示例
console.log(StringUtils.capitalize('hello'));  // "Hello"
console.log(StringUtils.toCamelCase('hello_world'));  // "helloWorld"
console.log(StringUtils.truncate('Hello World', 8));  // "Hello..."
console.log(StringUtils.format('Hello {0}!', 'World'));  // "Hello World!"
```

### 2. 模板引擎

```javascript
class TemplateEngine {
    static compile(template) {
        return function(data) {
            return template.replace(/\${(.*?)}/g, (match, key) => {
                return data[key.trim()] || '';
            });
        };
    }
    
    static render(template, data) {
        const compiled = this.compile(template);
        return compiled(data);
    }
}

// 使用示例
const template = '你好，${name}！今年${age}岁了。';
const data = { name: '张三', age: 25 };
console.log(TemplateEngine.render(template, data));
// "你好，张三！今年25岁了。"
```

## 最佳实践

1. 字符串连接
   ```javascript
   // 推荐：使用模板字符串
   const name = '张三';
   const greeting = `你好，${name}！`;
   
   // 推荐：大量字符串连接使用数组join
   const items = ['Hello', 'World'];
   const result = items.join(' ');
   ```

2. 正则表达式
   ```javascript
   // 推荐：预编译正则表达式
   const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
   
   function validateEmail(email) {
       return emailRegex.test(email);
   }
   ```

3. 性能优化
   ```javascript
   // 推荐：缓存字符串长度
   const str = 'Hello World';
   const len = str.length;
   for (let i = 0; i < len; i++) {
       // 使用str[i]
   }
   ```

## 总结

- 掌握基本字符串方法
- 熟练使用查找和提取方法
- 灵活运用修改方法
- 掌握正则表达式方法
- 理解字符串转换
- 应用最佳实践

下一章将介绍JavaScript字符串搜索。
