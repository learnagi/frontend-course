---
title: "JavaScript数字"
slug: "javascript-numbers"
sequence: 20
description: "详细介绍JavaScript数字的类型、属性和使用方法"
is_published: true
estimated_minutes: 25
language: "zh-CN"
---

# JavaScript数字

## 数字类型

### 1. 基本数字类型

```javascript
// 整数
const int1 = 42;
const int2 = -42;

// 浮点数
const float1 = 3.14;
const float2 = -3.14;

// 科学记数法
const sci1 = 123e5;    // 12300000
const sci2 = 123e-5;   // 0.00123

// 特殊值
const infinity = Infinity;
const negInfinity = -Infinity;
const notANumber = NaN;
```

### 2. BigInt类型

```javascript
// 创建BigInt
const bigInt1 = 9007199254740991n;
const bigInt2 = BigInt(9007199254740991);

// BigInt运算
const sum = bigInt1 + BigInt(1);
const product = bigInt1 * 2n;

// 注意：不能混合使用BigInt和普通数字
// 这会抛出TypeError
// const mixed = bigInt1 + 1;
```

## 数字表示

### 1. 进制表示

```javascript
// 十进制
const decimal = 42;

// 二进制（0b前缀）
const binary = 0b101010;     // 42

// 八进制（0o前缀）
const octal = 0o52;          // 42

// 十六进制（0x前缀）
const hex = 0x2A;            // 42

// 进制转换
console.log(decimal.toString(2));  // "101010"
console.log(decimal.toString(8));  // "52"
console.log(decimal.toString(16)); // "2a"
```

### 2. 数字精度

```javascript
// 浮点数精度问题
console.log(0.1 + 0.2);        // 0.30000000000000004
console.log(0.1 + 0.2 === 0.3); // false

// 处理精度问题
function add(num1, num2) {
    const precision = 100000;
    return Math.round((num1 + num2) * precision) / precision;
}

console.log(add(0.1, 0.2));    // 0.3

// 使用toFixed
const price = 19.99;
console.log(price.toFixed(2));  // "19.99"
```

## 数字操作

### 1. 基本运算

```javascript
// 算术运算
const a = 10;
const b = 3;

console.log(a + b);  // 13
console.log(a - b);  // 7
console.log(a * b);  // 30
console.log(a / b);  // 3.3333...
console.log(a % b);  // 1
console.log(a ** b); // 1000 (幂运算)

// 自增和自减
let count = 0;
console.log(++count);  // 1
console.log(count++);  // 1 (返回后增加)
console.log(--count);  // 1
console.log(count--);  // 1 (返回后减少)
```

### 2. Math对象方法

```javascript
// 基本数学运算
console.log(Math.abs(-5));     // 5
console.log(Math.round(3.7));  // 4
console.log(Math.ceil(3.2));   // 4
console.log(Math.floor(3.8));  // 3
console.log(Math.trunc(3.8));  // 3

// 最大值和最小值
console.log(Math.max(1, 2, 3));  // 3
console.log(Math.min(1, 2, 3));  // 1

// 幂运算和平方根
console.log(Math.pow(2, 3));     // 8
console.log(Math.sqrt(16));      // 4
console.log(Math.cbrt(27));      // 3

// 随机数
console.log(Math.random());      // 0到1之间的随机数
```

## 数字转换

### 1. 类型转换

```javascript
// 字符串转数字
console.log(Number('123'));     // 123
console.log(parseInt('123'));   // 123
console.log(parseFloat('3.14')); // 3.14
console.log(+'123');           // 123

// 数字转字符串
console.log(String(123));      // "123"
console.log((123).toString()); // "123"
console.log(123 + '');        // "123"

// 布尔值转换
console.log(Number(true));     // 1
console.log(Number(false));    // 0
```

### 2. 进制转换

```javascript
// 其他进制转十进制
console.log(parseInt('1010', 2));  // 10
console.log(parseInt('52', 8));    // 42
console.log(parseInt('2A', 16));   // 42

// 十进制转其他进制
const num = 42;
console.log(num.toString(2));      // "101010"
console.log(num.toString(8));      // "52"
console.log(num.toString(16));     // "2a"
```

## 数字格式化

### 1. 本地化格式

```javascript
// 使用Intl.NumberFormat
const formatter = new Intl.NumberFormat('zh-CN', {
    style: 'currency',
    currency: 'CNY'
});

console.log(formatter.format(123456.789));
// ¥123,456.79

// 不同地区格式
const formats = {
    'zh-CN': new Intl.NumberFormat('zh-CN'),
    'en-US': new Intl.NumberFormat('en-US'),
    'de-DE': new Intl.NumberFormat('de-DE')
};

const number = 123456.789;
console.log(formats['zh-CN'].format(number)); // 123,456.789
console.log(formats['en-US'].format(number)); // 123,456.789
console.log(formats['de-DE'].format(number)); // 123.456,789
```

### 2. 自定义格式化

```javascript
// 数字千分位格式化
function formatNumber(num) {
    return num.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ',');
}

// 金额格式化
function formatCurrency(amount, currency = 'CNY', locale = 'zh-CN') {
    return new Intl.NumberFormat(locale, {
        style: 'currency',
        currency: currency
    }).format(amount);
}

// 百分比格式化
function formatPercent(number, decimals = 2) {
    return `${(number * 100).toFixed(decimals)}%`;
}
```

## 实践应用

### 1. 金融计算

```javascript
class Financial {
    // 处理JavaScript浮点数精度问题
    static precise(num) {
        return parseFloat(num.toPrecision(12));
    }
    
    // 加法
    static add(...numbers) {
        const sum = numbers.reduce((acc, val) => {
            const decimalPlaces = (val.toString().split('.')[1] || '').length;
            const multiplier = Math.pow(10, decimalPlaces);
            return acc + val * multiplier;
        }, 0);
        
        const maxDecimalPlaces = Math.max(...numbers.map(n => 
            (n.toString().split('.')[1] || '').length
        ));
        
        return this.precise(sum / Math.pow(10, maxDecimalPlaces));
    }
    
    // 复利计算
    static compound(principal, rate, time, frequency = 1) {
        return this.precise(
            principal * Math.pow(1 + rate / frequency, frequency * time)
        );
    }
    
    // 年化收益率
    static annualReturn(startValue, endValue, years) {
        return this.precise(
            Math.pow(endValue / startValue, 1 / years) - 1
        );
    }
}
```

### 2. 统计计算

```javascript
class Statistics {
    // 平均值
    static mean(numbers) {
        return numbers.reduce((sum, num) => sum + num, 0) / numbers.length;
    }
    
    // 中位数
    static median(numbers) {
        const sorted = [...numbers].sort((a, b) => a - b);
        const middle = Math.floor(sorted.length / 2);
        
        if (sorted.length % 2 === 0) {
            return (sorted[middle - 1] + sorted[middle]) / 2;
        }
        
        return sorted[middle];
    }
    
    // 标准差
    static standardDeviation(numbers) {
        const mean = this.mean(numbers);
        const variance = numbers.reduce((sum, num) => {
            return sum + Math.pow(num - mean, 2);
        }, 0) / numbers.length;
        
        return Math.sqrt(variance);
    }
    
    // 众数
    static mode(numbers) {
        const counts = new Map();
        let maxCount = 0;
        let modes = [];
        
        numbers.forEach(num => {
            const count = (counts.get(num) || 0) + 1;
            counts.set(num, count);
            
            if (count > maxCount) {
                maxCount = count;
                modes = [num];
            } else if (count === maxCount) {
                modes.push(num);
            }
        });
        
        return modes;
    }
}
```

## 最佳实践

1. 数字处理
   ```javascript
   // 推荐：使用Number类型转换
   const value = Number('123');
   
   // 推荐：处理浮点数精度
   const result = parseFloat((0.1 + 0.2).toFixed(10));
   ```

2. 性能优化
   ```javascript
   // 推荐：使用位运算
   const floor = num => num >> 0;
   const ceil = num => (num + 0.999999) >> 0;
   
   // 推荐：缓存数学计算
   const PI2 = Math.PI * 2;
   ```

3. 安全性考虑
   ```javascript
   // 推荐：检查是否是有效数字
   function isValidNumber(num) {
       return typeof num === 'number' && 
              !isNaN(num) && 
              isFinite(num);
   }
   ```

## 总结

- 掌握数字类型
- 理解数字表示
- 熟练数字操作
- 处理数字转换
- 实现格式化
- 应用实践案例

下一章将介绍JavaScript BigInt。
