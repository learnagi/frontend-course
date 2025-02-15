---
title: "JavaScript BigInt"
slug: "javascript-bigint"
sequence: 21
description: "详细介绍JavaScript BigInt的使用方法和应用场景"
is_published: true
estimated_minutes: 25
language: "zh-CN"
---

# JavaScript BigInt

## BigInt基础

### 1. 什么是BigInt

```javascript
// BigInt是JavaScript的一种内置数字类型
// 可以表示任意精度的整数

// Number类型的最大安全整数
console.log(Number.MAX_SAFE_INTEGER);  // 9007199254740991

// 超过最大安全整数的计算会不准确
console.log(9007199254740991 + 1);     // 9007199254740992
console.log(9007199254740991 + 2);     // 9007199254740992 (错误)

// 使用BigInt可以精确处理大整数
console.log(9007199254740991n + 1n);   // 9007199254740992n
console.log(9007199254740991n + 2n);   // 9007199254740993n
```

### 2. 创建BigInt

```javascript
// 使用n后缀
const bigInt1 = 123n;
const bigInt2 = 9007199254740991n;

// 使用BigInt()构造函数
const bigInt3 = BigInt(123);
const bigInt4 = BigInt("9007199254740991");

// 使用其他进制
const binaryBigInt = BigInt("0b1010");  // 10n
const octalBigInt = BigInt("0o12");     // 10n
const hexBigInt = BigInt("0xa");        // 10n
```

## BigInt操作

### 1. 基本运算

```javascript
// 加法
console.log(1n + 2n);     // 3n

// 减法
console.log(3n - 2n);     // 1n

// 乘法
console.log(2n * 3n);     // 6n

// 除法
console.log(6n / 2n);     // 3n
// 注意：BigInt除法会向零取整
console.log(5n / 2n);     // 2n

// 求余
console.log(5n % 2n);     // 1n

// 幂运算
console.log(2n ** 3n);    // 8n

// 一元操作
console.log(-3n);         // -3n
console.log(+3n);        // TypeError: Cannot convert BigInt to number
```

### 2. 比较操作

```javascript
// 相等比较
console.log(1n === 1);    // false
console.log(1n == 1);     // true

// 大小比较
console.log(1n < 2);      // true
console.log(2n > 1);      // true
console.log(2n >= 2);     // true
console.log(2n <= 2);     // true

// 排序
const mixed = [3n, 4, 7n, 1, 2n];
mixed.sort((a, b) => {
    return a < b ? -1 : a > b ? 1 : 0;
});
console.log(mixed);  // [1, 2n, 3n, 4, 7n]
```

## 类型转换

### 1. BigInt转换

```javascript
// BigInt转Number
console.log(Number(123n));                    // 123
console.log(Number(9007199254740993n));      // 9007199254740992 (精度丢失)

// BigInt转String
console.log(String(123n));                    // "123"
console.log(123n.toString());                 // "123"
console.log(123n.toString(2));               // "1111011" (二进制)
console.log(123n.toString(16));              // "7b" (十六进制)

// String转BigInt
console.log(BigInt("123"));                   // 123n
console.log(BigInt("0x7B"));                  // 123n
console.log(BigInt("0b1111011"));            // 123n

// Boolean转BigInt
console.log(BigInt(true));                    // 1n
console.log(BigInt(false));                   // 0n
```

### 2. 注意事项

```javascript
// 不能使用Math对象的方法
try {
    Math.max(1n, 2n);
} catch (e) {
    console.log(e);  // TypeError: Cannot convert BigInt to number
}

// 不能与Number混合运算
try {
    1n + 1;
} catch (e) {
    console.log(e);  // TypeError: Cannot mix BigInt and other types
}

// 不能使用一元加号运算符
try {
    +1n;
} catch (e) {
    console.log(e);  // TypeError: Cannot convert BigInt to number
}
```

## 实践应用

### 1. 大整数计算

```javascript
class BigIntCalculator {
    // 阶乘计算
    static factorial(n) {
        if (typeof n !== 'bigint') {
            n = BigInt(n);
        }
        
        if (n < 0n) {
            throw new Error('Factorial not defined for negative numbers');
        }
        
        let result = 1n;
        for (let i = 2n; i <= n; i++) {
            result *= i;
        }
        return result;
    }
    
    // 斐波那契数列
    static fibonacci(n) {
        if (typeof n !== 'bigint') {
            n = BigInt(n);
        }
        
        if (n < 0n) {
            throw new Error('Index cannot be negative');
        }
        
        let prev = 0n;
        let current = 1n;
        
        for (let i = 0n; i < n; i++) {
            [prev, current] = [current, prev + current];
        }
        
        return prev;
    }
    
    // 最大公约数
    static gcd(a, b) {
        a = BigInt(a);
        b = BigInt(b);
        
        while (b) {
            [a, b] = [b, a % b];
        }
        
        return a;
    }
}
```

### 2. 密码学应用

```javascript
class CryptoUtils {
    // 生成大素数
    static isPrime(n) {
        if (n <= 1n) return false;
        if (n <= 3n) return true;
        if (n % 2n === 0n) return false;
        
        const sqrt = this.sqrt(n);
        for (let i = 3n; i <= sqrt; i += 2n) {
            if (n % i === 0n) return false;
        }
        
        return true;
    }
    
    // 平方根（向下取整）
    static sqrt(value) {
        if (value < 0n) {
            throw new Error('Square root of negative numbers is not supported');
        }
        
        if (value < 2n) {
            return value;
        }
        
        let x0 = value / 2n;
        let x1 = (x0 + value / x0) / 2n;
        
        while (x1 < x0) {
            x0 = x1;
            x1 = (x0 + value / x0) / 2n;
        }
        
        return x0;
    }
    
    // 模幂运算 (a^b mod m)
    static modPow(base, exponent, modulus) {
        if (modulus === 1n) return 0n;
        
        base = BigInt(base);
        exponent = BigInt(exponent);
        modulus = BigInt(modulus);
        
        let result = 1n;
        base = base % modulus;
        
        while (exponent > 0n) {
            if (exponent % 2n === 1n) {
                result = (result * base) % modulus;
            }
            base = (base * base) % modulus;
            exponent = exponent / 2n;
        }
        
        return result;
    }
}
```

## 性能优化

### 1. 计算优化

```javascript
// 优化BigInt计算
class BigIntOptimizer {
    // 快速幂算法
    static fastPow(base, exponent) {
        if (exponent === 0n) return 1n;
        if (exponent === 1n) return base;
        
        const half = this.fastPow(base, exponent / 2n);
        if (exponent % 2n === 0n) {
            return half * half;
        }
        return half * half * base;
    }
    
    // 分块处理大数组
    static sumArray(arr, blockSize = 1000) {
        const bigInts = arr.map(n => BigInt(n));
        let sum = 0n;
        
        for (let i = 0; i < bigInts.length; i += blockSize) {
            const block = bigInts.slice(i, i + blockSize);
            sum += block.reduce((acc, val) => acc + val, 0n);
        }
        
        return sum;
    }
}
```

### 2. 内存优化

```javascript
// 内存优化技巧
class MemoryOptimizer {
    // 使用生成器处理大数列
    static *generateRange(start, end, step = 1n) {
        for (let i = BigInt(start); i < BigInt(end); i += BigInt(step)) {
            yield i;
        }
    }
    
    // 使用迭代器处理大数组
    static *chunkArray(arr, size) {
        const bigInts = arr.map(n => BigInt(n));
        for (let i = 0; i < bigInts.length; i += size) {
            yield bigInts.slice(i, i + size);
        }
    }
}
```

## 最佳实践

1. 类型检查
   ```javascript
   // 推荐：检查是否是BigInt
   function isBigInt(value) {
       return typeof value === 'bigint';
   }
   
   // 推荐：安全转换
   function safeToBigInt(value) {
       try {
           return BigInt(value);
       } catch (e) {
           return null;
       }
   }
   ```

2. 错误处理
   ```javascript
   // 推荐：处理BigInt运算错误
   function safeBigIntOperation(operation, ...args) {
       try {
           return operation(...args);
       } catch (e) {
           console.error('BigInt operation failed:', e);
           return null;
       }
   }
   ```

3. 格式化输出
   ```javascript
   // 推荐：格式化BigInt显示
   function formatBigInt(bigint, groupSize = 3) {
       const str = bigint.toString();
       const regex = new RegExp(`\\B(?=(\\d{${groupSize}})+(?!\\d))`, 'g');
       return str.replace(regex, ',');
   }
   ```

## 总结

- 理解BigInt特性
- 掌握基本操作
- 处理类型转换
- 实现实践应用
- 优化性能
- 遵循最佳实践

下一章将介绍JavaScript数字方法。
