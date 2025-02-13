---
title: "JavaScript算术运算"
slug: "javascript-arithmetic"
sequence: 7
description: "深入了解JavaScript的算术运算和数学计算"
is_published: true
estimated_minutes: 25
language: "zh-CN"
---

# JavaScript算术运算

## 基本算术运算

### 1. 数值运算

```javascript
// 加法
let sum = 5 + 3;        // 8
let negativeSum = -5 + 3; // -2

// 减法
let difference = 10 - 5;  // 5
let negative = 5 - 10;    // -5

// 乘法
let product = 4 * 3;      // 12
let decimal = 0.1 * 0.2;  // 0.020000000000000004（注意精度问题）

// 除法
let quotient = 15 / 3;    // 5
let decimal2 = 10 / 3;    // 3.3333333333333335

// 取余（模运算）
let remainder = 17 % 5;   // 2
let negRemainder = -17 % 5; // -2

// 幂运算
let power = 2 ** 3;       // 8
let squareRoot = 16 ** 0.5; // 4（开平方）
```

### 2. 数字精度

```javascript
// 处理小数精度问题
let result = 0.1 + 0.2;           // 0.30000000000000004
let fixed = (0.1 + 0.2).toFixed(2); // "0.30"

// 使用Number.EPSILON比较小数
function nearlyEqual(a, b) {
    return Math.abs(a - b) < Number.EPSILON;
}

console.log(nearlyEqual(0.1 + 0.2, 0.3)); // true

// 处理大数字
console.log(Number.MAX_SAFE_INTEGER);  // 9007199254740991
console.log(Number.MIN_SAFE_INTEGER);  // -9007199254740991

// 使用BigInt处理大数字
let bigNumber = 9007199254740991n + 1n;
```

## Math对象

### 1. 数学常量

```javascript
// 常用数学常量
console.log(Math.PI);      // 3.141592653589793
console.log(Math.E);       // 2.718281828459045
console.log(Math.SQRT2);   // 1.4142135623730951
console.log(Math.LN2);     // 0.6931471805599453
console.log(Math.LN10);    // 2.302585092994046
```

### 2. 数学函数

```javascript
// 取整函数
console.log(Math.round(3.6));  // 4（四舍五入）
console.log(Math.ceil(3.1));   // 4（向上取整）
console.log(Math.floor(3.9));  // 3（向下取整）
console.log(Math.trunc(3.9));  // 3（去除小数部分）

// 最值函数
console.log(Math.max(1, 5, 3));     // 5
console.log(Math.min(1, 5, 3));     // 1
console.log(Math.max(...[1, 5, 3])); // 5

// 绝对值
console.log(Math.abs(-5));    // 5
console.log(Math.abs(5));     // 5

// 幂运算和开方
console.log(Math.pow(2, 3));     // 8
console.log(Math.sqrt(16));      // 4
console.log(Math.cbrt(27));      // 3（立方根）

// 随机数
console.log(Math.random());          // 0到1之间的随机数
```

## 实用数学计算

### 1. 生成随机数

```javascript
// 生成指定范围的随机整数
function getRandomInt(min, max) {
    min = Math.ceil(min);
    max = Math.floor(max);
    return Math.floor(Math.random() * (max - min + 1)) + min;
}

// 生成随机颜色
function getRandomColor() {
    return '#' + Math.floor(Math.random()*16777215).toString(16);
}

// 生成随机ID
function generateId(length = 8) {
    return Math.random().toString(36).substr(2, length);
}
```

### 2. 金融计算

```javascript
// 处理货币计算
function formatMoney(amount) {
    return new Intl.NumberFormat('zh-CN', {
        style: 'currency',
        currency: 'CNY'
    }).format(amount);
}

// 计算复利
function compound(principal, rate, years) {
    return principal * Math.pow(1 + rate, years);
}

// 处理精确计算
function add(a, b) {
    const multiplier = Math.pow(10, 10);
    return Math.round((a + b) * multiplier) / multiplier;
}
```

### 3. 几何计算

```javascript
// 计算圆的面积
function circleArea(radius) {
    return Math.PI * radius ** 2;
}

// 计算两点之间的距离
function distance(x1, y1, x2, y2) {
    return Math.sqrt((x2 - x1) ** 2 + (y2 - y1) ** 2);
}

// 角度与弧度转换
function toRadians(degrees) {
    return degrees * (Math.PI / 180);
}

function toDegrees(radians) {
    return radians * (180 / Math.PI);
}
```

## 数值格式化

### 1. 数字格式化

```javascript
// 使用toFixed
let num = 123.456;
console.log(num.toFixed(2));     // "123.46"

// 使用toPrecision
console.log(num.toPrecision(4)); // "123.5"

// 使用Intl.NumberFormat
const formatter = new Intl.NumberFormat('zh-CN');
console.log(formatter.format(123456.789)); // "123,456.789"

// 格式化百分比
const percentFormatter = new Intl.NumberFormat('zh-CN', {
    style: 'percent',
    minimumFractionDigits: 2
});
console.log(percentFormatter.format(0.1234)); // "12.34%"
```

### 2. 单位转换

```javascript
// 文件大小转换
function formatFileSize(bytes) {
    const units = ['B', 'KB', 'MB', 'GB', 'TB'];
    let size = bytes;
    let unitIndex = 0;
    
    while (size >= 1024 && unitIndex < units.length - 1) {
        size /= 1024;
        unitIndex++;
    }
    
    return `${size.toFixed(2)} ${units[unitIndex]}`;
}

// 时间转换
function formatDuration(seconds) {
    const hours = Math.floor(seconds / 3600);
    const minutes = Math.floor((seconds % 3600) / 60);
    const remainingSeconds = seconds % 60;
    
    return `${hours}:${minutes.toString().padStart(2, '0')}:${remainingSeconds.toString().padStart(2, '0')}`;
}
```

## 最佳实践

1. 处理精度问题
   ```javascript
   // 使用乘法和除法避免浮点数问题
   function calculatePrice(price, quantity) {
       return Math.round(price * 100 * quantity) / 100;
   }
   ```

2. 安全的数值转换
   ```javascript
   // 使用Number()或parseFloat()进行转换
   function safeParseNumber(value) {
       const num = Number(value);
       return isNaN(num) ? 0 : num;
   }
   ```

3. 范围检查
   ```javascript
   function clamp(number, min, max) {
       return Math.min(Math.max(number, min), max);
   }
   ```

## 练习

```javascript
// 1. 实现一个简单的计算器
class Calculator {
    static add(a, b) {
        return Number((a + b).toFixed(10));
    }
    
    static subtract(a, b) {
        return Number((a - b).toFixed(10));
    }
    
    static multiply(a, b) {
        return Number((a * b).toFixed(10));
    }
    
    static divide(a, b) {
        if (b === 0) throw new Error("除数不能为零");
        return Number((a / b).toFixed(10));
    }
}

// 2. 实现数组的数学计算
class ArrayMath {
    static sum(arr) {
        return arr.reduce((a, b) => Calculator.add(a, b), 0);
    }
    
    static average(arr) {
        if (arr.length === 0) return 0;
        return Calculator.divide(this.sum(arr), arr.length);
    }
    
    static standardDeviation(arr) {
        const avg = this.average(arr);
        const squareDiffs = arr.map(value => 
            Calculator.multiply(
                Calculator.subtract(value, avg),
                Calculator.subtract(value, avg)
            )
        );
        return Math.sqrt(this.average(squareDiffs));
    }
}
```

## 总结

- 理解基本算术运算
- 掌握Math对象的使用
- 处理数值精度问题
- 实现常用数学计算
- 正确格式化数值
- 注意数值计算的安全性

下一章将介绍JavaScript的赋值运算。
