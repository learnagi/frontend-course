---
title: "JavaScript数字属性"
slug: "javascript-number-properties"
sequence: 23
description: "详细介绍JavaScript数字的属性及其使用方法"
is_published: true
estimated_minutes: 25
language: "zh-CN"
---

# JavaScript数字属性

## Number对象属性

### 1. 数值范围

```javascript
// 最大值
console.log(Number.MAX_VALUE);        // 1.7976931348623157e+308
console.log(Number.MIN_VALUE);        // 5e-324

// 最大安全整数
console.log(Number.MAX_SAFE_INTEGER); // 9007199254740991
console.log(Number.MIN_SAFE_INTEGER); // -9007199254740991

// 正无穷和负无穷
console.log(Number.POSITIVE_INFINITY); // Infinity
console.log(Number.NEGATIVE_INFINITY); // -Infinity

// 非数值
console.log(Number.NaN);              // NaN
```

### 2. 精度相关

```javascript
// EPSILON - 表示1与大于1的最小浮点数之间的差值
console.log(Number.EPSILON);          // 2.220446049250313e-16

// 使用EPSILON比较浮点数
function areEqual(a, b) {
    return Math.abs(a - b) < Number.EPSILON;
}

console.log(areEqual(0.1 + 0.2, 0.3));  // true
```

## Math对象属性

### 1. 数学常量

```javascript
// 圆周率
console.log(Math.PI);        // 3.141592653589793

// 自然对数的底数
console.log(Math.E);         // 2.718281828459045

// 2的自然对数
console.log(Math.LN2);       // 0.6931471805599453

// 10的自然对数
console.log(Math.LN10);      // 2.302585092994046

// 以2为底的e的对数
console.log(Math.LOG2E);     // 1.4426950408889634

// 以10为底的e的对数
console.log(Math.LOG10E);    // 0.4342944819032518
```

### 2. 常用数学常量

```javascript
// 常用的派生常量
const mathConstants = {
    // 圆相关
    TWO_PI: 2 * Math.PI,           // 2π
    HALF_PI: Math.PI / 2,          // π/2
    QUARTER_PI: Math.PI / 4,       // π/4
    
    // 角度转换
    DEG_TO_RAD: Math.PI / 180,     // 角度转弧度
    RAD_TO_DEG: 180 / Math.PI,     // 弧度转角度
    
    // 黄金分割比
    GOLDEN_RATIO: (1 + Math.sqrt(5)) / 2,  // ≈ 1.618033988749895
    
    // 自然对数
    LN2_INV: 1 / Math.LN2,         // 1/ln(2)
    LN10_INV: 1 / Math.LN10        // 1/ln(10)
};
```

## 属性应用

### 1. 数值检查

```javascript
class NumberValidator {
    // 检查是否超出安全整数范围
    static isSafeInteger(num) {
        return Number.isSafeInteger(num);
    }
    
    // 检查是否在指定范围内
    static isInRange(num, min, max) {
        return num >= min && num <= max;
    }
    
    // 检查是否为有限数
    static isFinite(num) {
        return Number.isFinite(num);
    }
    
    // 检查是否接近某个值
    static isCloseTo(a, b, tolerance = Number.EPSILON) {
        return Math.abs(a - b) < tolerance;
    }
}
```

### 2. 数值转换

```javascript
class NumberConverter {
    // 角度转弧度
    static degreesToRadians(degrees) {
        return degrees * Math.PI / 180;
    }
    
    // 弧度转角度
    static radiansToDegrees(radians) {
        return radians * 180 / Math.PI;
    }
    
    // 确保数值在范围内
    static clamp(num, min, max) {
        return Math.min(Math.max(num, min), max);
    }
    
    // 将数值映射到新范围
    static map(num, inMin, inMax, outMin, outMax) {
        return (num - inMin) * (outMax - outMin) / (inMax - inMin) + outMin;
    }
}
```

## 实践应用

### 1. 科学计算

```javascript
class ScientificCalculator {
    // 计算圆的面积
    static circleArea(radius) {
        return Math.PI * radius * radius;
    }
    
    // 计算球体体积
    static sphereVolume(radius) {
        return (4/3) * Math.PI * Math.pow(radius, 3);
    }
    
    // 计算对数
    static logarithm(value, base = Math.E) {
        return Math.log(value) / Math.log(base);
    }
    
    // 计算复数的模
    static complexMagnitude(real, imaginary) {
        return Math.sqrt(real * real + imaginary * imaginary);
    }
}
```

### 2. 金融计算

```javascript
class FinancialConstants {
    static DAYS_IN_YEAR = 365;
    static MONTHS_IN_YEAR = 12;
    static STANDARD_PAYMENT_FREQUENCY = 12;
    
    // 利率转换
    static annualToMonthlyRate(annualRate) {
        return Math.pow(1 + annualRate, 1/this.MONTHS_IN_YEAR) - 1;
    }
    
    // 日利率转换
    static annualToDailyRate(annualRate) {
        return Math.pow(1 + annualRate, 1/this.DAYS_IN_YEAR) - 1;
    }
    
    // 检查利率是否在合理范围内
    static isValidInterestRate(rate) {
        return rate >= 0 && rate <= 1 && Number.isFinite(rate);
    }
}
```

### 3. 性能优化

```javascript
class MathOptimizer {
    // 缓存常用数学常量
    static Constants = {
        TWO_PI: 2 * Math.PI,
        HALF_PI: Math.PI / 2,
        QUARTER_PI: Math.PI / 4,
        ONE_OVER_PI: 1 / Math.PI,
        ONE_OVER_TWO_PI: 1 / (2 * Math.PI),
        SQRT2: Math.sqrt(2),
        SQRT3: Math.sqrt(3),
        ONE_OVER_SQRT2: 1 / Math.sqrt(2)
    };
    
    // 使用位运算优化
    static isPowerOfTwo(n) {
        return n > 0 && (n & (n - 1)) === 0;
    }
    
    static isEven(n) {
        return (n & 1) === 0;
    }
    
    static floorLog2(n) {
        return 31 - Math.clz32(n);
    }
}
```

## 最佳实践

1. 常量定义
   ```javascript
   // 推荐：使用常量对象
   const MathConstants = Object.freeze({
       PI: Math.PI,
       E: Math.E,
       GOLDEN_RATIO: (1 + Math.sqrt(5)) / 2,
       DEG_TO_RAD: Math.PI / 180,
       RAD_TO_DEG: 180 / Math.PI
   });
   ```

2. 范围检查
   ```javascript
   // 推荐：安全的数值检查
   function isSafeNumber(value) {
       return Number.isFinite(value) &&
              value >= Number.MIN_SAFE_INTEGER &&
              value <= Number.MAX_SAFE_INTEGER;
   }
   ```

3. 精度处理
   ```javascript
   // 推荐：处理浮点数比较
   function approximatelyEqual(a, b, epsilon = Number.EPSILON) {
       return Math.abs(a - b) < epsilon;
   }
   ```

## 总结

- 了解Number属性
- 掌握Math属性
- 应用数学常量
- 实现数值检查
- 优化计算性能
- 遵循最佳实践

下一章将介绍JavaScript数组。
