---
title: "JavaScript数字方法"
slug: "javascript-number-methods"
sequence: 22
description: "详细介绍JavaScript数字的各种方法及其使用"
is_published: true
estimated_minutes: 25
language: "zh-CN"
---

# JavaScript数字方法

## Number对象方法

### 1. 数字验证

```javascript
// isInteger - 检查是否为整数
console.log(Number.isInteger(5));     // true
console.log(Number.isInteger(5.0));   // true
console.log(Number.isInteger(5.1));   // false

// isFinite - 检查是否为有限数
console.log(Number.isFinite(123));     // true
console.log(Number.isFinite(Infinity)); // false
console.log(Number.isFinite(NaN));     // false

// isNaN - 检查是否为NaN
console.log(Number.isNaN(NaN));       // true
console.log(Number.isNaN(123));       // false
console.log(Number.isNaN('123'));     // false

// isSafeInteger - 检查是否为安全整数
console.log(Number.isSafeInteger(123));                    // true
console.log(Number.isSafeInteger(9007199254740991));      // true
console.log(Number.isSafeInteger(9007199254740992));      // false
```

### 2. 数字转换

```javascript
// parseInt - 将字符串转换为整数
console.log(Number.parseInt('123'));      // 123
console.log(Number.parseInt('123.45'));   // 123
console.log(Number.parseInt('123abc'));   // 123
console.log(Number.parseInt('abc123'));   // NaN

// parseFloat - 将字符串转换为浮点数
console.log(Number.parseFloat('123.45')); // 123.45
console.log(Number.parseFloat('123'));    // 123
console.log(Number.parseFloat('abc'));    // NaN

// 进制转换
console.log(Number.parseInt('1010', 2));  // 10
console.log(Number.parseInt('ff', 16));   // 255
```

## 实例方法

### 1. 格式化方法

```javascript
// toFixed - 指定小数位数
const num = 123.456789;
console.log(num.toFixed(2));     // "123.46"
console.log(num.toFixed(0));     // "123"
console.log(num.toFixed(5));     // "123.45679"

// toPrecision - 指定有效数字位数
console.log(num.toPrecision(4)); // "123.5"
console.log(num.toPrecision(2)); // "1.2e+2"
console.log(num.toPrecision(8)); // "123.45679"

// toExponential - 科学记数法
console.log(num.toExponential());  // "1.23456789e+2"
console.log(num.toExponential(2)); // "1.23e+2"
console.log(num.toExponential(5)); // "1.23457e+2"
```

### 2. 转换方法

```javascript
// toString - 转换为字符串
const num = 255;
console.log(num.toString());     // "255"
console.log(num.toString(2));    // "11111111" (二进制)
console.log(num.toString(16));   // "ff" (十六进制)

// valueOf - 返回原始值
const numObj = new Number(123);
console.log(numObj.valueOf());   // 123
```

## Math对象方法

### 1. 基本数学运算

```javascript
// 绝对值
console.log(Math.abs(-5));      // 5

// 向上取整
console.log(Math.ceil(4.3));    // 5
console.log(Math.ceil(-4.3));   // -4

// 向下取整
console.log(Math.floor(4.7));   // 4
console.log(Math.floor(-4.7));  // -5

// 四舍五入
console.log(Math.round(4.3));   // 4
console.log(Math.round(4.7));   // 5

// 截断小数
console.log(Math.trunc(4.7));   // 4
console.log(Math.trunc(-4.7));  // -4
```

### 2. 高级数学运算

```javascript
// 幂运算
console.log(Math.pow(2, 3));    // 8
console.log(Math.pow(4, 0.5));  // 2

// 平方根
console.log(Math.sqrt(16));     // 4
console.log(Math.sqrt(2));      // 1.4142135623730951

// 立方根
console.log(Math.cbrt(27));     // 3
console.log(Math.cbrt(-27));    // -3

// 最大值和最小值
console.log(Math.max(1, 2, 3));  // 3
console.log(Math.min(1, 2, 3));  // 1

// 随机数
console.log(Math.random());      // 0到1之间的随机数
```

### 3. 三角函数

```javascript
// 正弦
console.log(Math.sin(Math.PI / 2));  // 1

// 余弦
console.log(Math.cos(Math.PI));      // -1

// 正切
console.log(Math.tan(Math.PI / 4));  // ~1

// 反正弦
console.log(Math.asin(1));           // π/2

// 反余弦
console.log(Math.acos(0));           // π/2

// 反正切
console.log(Math.atan(1));           // π/4
```

## 实践应用

### 1. 数学计算工具

```javascript
class MathUtils {
    // 计算平均值
    static mean(numbers) {
        return numbers.reduce((sum, num) => sum + num, 0) / numbers.length;
    }
    
    // 计算标准差
    static standardDeviation(numbers) {
        const mean = this.mean(numbers);
        const variance = numbers.reduce((sum, num) => {
            return sum + Math.pow(num - mean, 2);
        }, 0) / numbers.length;
        return Math.sqrt(variance);
    }
    
    // 生成指定范围的随机整数
    static randomInt(min, max) {
        return Math.floor(Math.random() * (max - min + 1)) + min;
    }
    
    // 计算百分比
    static percentage(value, total, decimals = 2) {
        return Number(((value / total) * 100).toFixed(decimals));
    }
}
```

### 2. 金融计算工具

```javascript
class FinancialCalculator {
    // 复利计算
    static compound(principal, rate, time, frequency = 1) {
        return principal * Math.pow(1 + rate / frequency, frequency * time);
    }
    
    // 贷款月供计算
    static monthlyPayment(principal, rate, years) {
        const monthlyRate = rate / 12;
        const months = years * 12;
        return principal * monthlyRate * Math.pow(1 + monthlyRate, months) / 
               (Math.pow(1 + monthlyRate, months) - 1);
    }
    
    // 现值计算
    static presentValue(futureValue, rate, time) {
        return futureValue / Math.pow(1 + rate, time);
    }
    
    // 年化收益率
    static annualReturn(startValue, endValue, years) {
        return Math.pow(endValue / startValue, 1 / years) - 1;
    }
}
```

### 3. 格式化工具

```javascript
class NumberFormatter {
    // 数字千分位格式化
    static format(num, locale = 'zh-CN') {
        return new Intl.NumberFormat(locale).format(num);
    }
    
    // 货币格式化
    static formatCurrency(amount, currency = 'CNY', locale = 'zh-CN') {
        return new Intl.NumberFormat(locale, {
            style: 'currency',
            currency: currency
        }).format(amount);
    }
    
    // 百分比格式化
    static formatPercent(num, decimals = 2, locale = 'zh-CN') {
        return new Intl.NumberFormat(locale, {
            style: 'percent',
            minimumFractionDigits: decimals,
            maximumFractionDigits: decimals
        }).format(num);
    }
    
    // 文件大小格式化
    static formatFileSize(bytes) {
        const units = ['B', 'KB', 'MB', 'GB', 'TB'];
        let size = bytes;
        let unitIndex = 0;
        
        while (size >= 1024 && unitIndex < units.length - 1) {
            size /= 1024;
            unitIndex++;
        }
        
        return `${size.toFixed(2)} ${units[unitIndex]}`;
    }
}
```

## 最佳实践

1. 数字验证
   ```javascript
   // 推荐：使用严格的数字验证
   function isValidNumber(value) {
       return typeof value === 'number' && 
              Number.isFinite(value) && 
              !Number.isNaN(value);
   }
   ```

2. 精度处理
   ```javascript
   // 推荐：处理浮点数精度问题
   function preciseCalculation(num1, num2, operation) {
       const precision = 100000;
       const n1 = Math.round(num1 * precision);
       const n2 = Math.round(num2 * precision);
       
       switch(operation) {
           case 'add':
               return (n1 + n2) / precision;
           case 'subtract':
               return (n1 - n2) / precision;
           case 'multiply':
               return (n1 * n2) / (precision * precision);
           case 'divide':
               return n1 / n2;
       }
   }
   ```

3. 性能优化
   ```javascript
   // 推荐：缓存数学常量
   const TWO_PI = 2 * Math.PI;
   const HALF_PI = Math.PI / 2;
   
   // 推荐：使用位运算
   const isEven = num => (num & 1) === 0;
   const isPowerOfTwo = num => num > 0 && (num & (num - 1)) === 0;
   ```

## 总结

- 掌握Number对象方法
- 熟练使用Math对象
- 处理数字格式化
- 实现数学计算
- 优化代码性能
- 遵循最佳实践

下一章将介绍JavaScript数字属性。
