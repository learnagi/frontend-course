---
title: "JavaScript函数"
slug: "javascript-functions"
sequence: 9
description: "详细介绍JavaScript函数的定义和使用方法"
is_published: true
estimated_minutes: 30
language: "zh-CN"
---

# JavaScript函数

## 函数定义

### 1. 函数声明

```javascript
// 基本函数声明
function sayHello() {
    console.log("Hello!");
}

// 带参数的函数
function greet(name) {
    console.log("Hello, " + name + "!");
}

// 带返回值的函数
function add(a, b) {
    return a + b;
}

// 带默认参数的函数
function greetUser(name = "Guest") {
    console.log("Welcome, " + name + "!");
}
```

### 2. 函数表达式

```javascript
// 匿名函数表达式
const sayHi = function() {
    console.log("Hi!");
};

// 命名函数表达式
const factorial = function fac(n) {
    return n < 2 ? 1 : n * fac(n - 1);
};

// 箭头函数
const square = (x) => x * x;
const greet = () => console.log("Hello!");
const sum = (a, b) => {
    let result = a + b;
    return result;
};
```

## 函数参数

### 1. 参数类型

```javascript
// 基本类型参数
function processNumber(num) {
    return num * 2;
}

// 对象参数
function updateUser(user) {
    user.name = user.name.toUpperCase();
}

// 数组参数
function sumArray(numbers) {
    return numbers.reduce((sum, num) => sum + num, 0);
}
```

### 2. 参数特性

```javascript
// 默认参数
function createUser(name = "匿名", age = 0) {
    return { name, age };
}

// 剩余参数
function sum(...numbers) {
    return numbers.reduce((total, num) => total + num, 0);
}

// 参数解构
function printUserInfo({ name, age, email = "未提供" }) {
    console.log(`姓名：${name}，年龄：${age}，邮箱：${email}`);
}
```

## 函数返回值

### 1. 返回类型

```javascript
// 返回单个值
function getMessage() {
    return "Hello World";
}

// 返回多个值（使用对象）
function getUserInfo() {
    return {
        name: "张三",
        age: 25,
        email: "zhangsan@example.com"
    };
}

// 返回多个值（使用数组）
function divide(a, b) {
    return [Math.floor(a / b), a % b];
}
```

### 2. 返回函数

```javascript
// 返回函数的函数（高阶函数）
function multiply(factor) {
    return function(number) {
        return number * factor;
    };
}

const double = multiply(2);
console.log(double(5)); // 10

// 返回箭头函数
function createGreeter(prefix) {
    return (name) => `${prefix}, ${name}!`;
}
```

## 函数作用域

### 1. 变量作用域

```javascript
// 全局作用域
let globalVar = "我是全局变量";

function testScope() {
    // 函数作用域
    let localVar = "我是局部变量";
    console.log(globalVar);  // 可以访问
    console.log(localVar);   // 可以访问
}

// console.log(localVar);  // 错误：localVar未定义

// 块级作用域
function blockScopeDemo() {
    let x = 1;
    
    if (true) {
        let y = 2;
        console.log(x); // 1
    }
    // console.log(y); // 错误：y未定义
}
```

### 2. 闭包

```javascript
// 基本闭包
function createCounter() {
    let count = 0;
    return {
        increment() {
            count++;
            return count;
        },
        decrement() {
            count--;
            return count;
        },
        getCount() {
            return count;
        }
    };
}

// 私有变量
function createUser(name) {
    let _name = name;  // 私有变量
    
    return {
        getName() {
            return _name;
        },
        setName(newName) {
            _name = newName;
        }
    };
}
```

## 函数高级特性

### 1. 递归

```javascript
// 阶乘计算
function factorial(n) {
    if (n <= 1) return 1;
    return n * factorial(n - 1);
}

// 深度克隆
function deepClone(obj) {
    if (obj === null || typeof obj !== "object") {
        return obj;
    }
    
    if (Array.isArray(obj)) {
        return obj.map(item => deepClone(item));
    }
    
    return Object.fromEntries(
        Object.entries(obj).map(([key, value]) => [
            key,
            deepClone(value)
        ])
    );
}
```

### 2. 函数柯里化

```javascript
// 基本柯里化
function curry(fn) {
    return function curried(...args) {
        if (args.length >= fn.length) {
            return fn.apply(this, args);
        }
        return function(...args2) {
            return curried.apply(this, args.concat(args2));
        };
    };
}

// 使用示例
function add(a, b, c) {
    return a + b + c;
}

const curriedAdd = curry(add);
console.log(curriedAdd(1)(2)(3)); // 6
```

## 实践示例

### 1. 防抖和节流

```javascript
// 防抖函数
function debounce(fn, delay) {
    let timer = null;
    return function(...args) {
        clearTimeout(timer);
        timer = setTimeout(() => {
            fn.apply(this, args);
        }, delay);
    };
}

// 节流函数
function throttle(fn, interval) {
    let last = 0;
    return function(...args) {
        const now = Date.now();
        if (now - last >= interval) {
            last = now;
            fn.apply(this, args);
        }
    };
}
```

### 2. 函数记忆

```javascript
// 记忆函数
function memoize(fn) {
    const cache = new Map();
    return function(...args) {
        const key = JSON.stringify(args);
        if (cache.has(key)) {
            return cache.get(key);
        }
        const result = fn.apply(this, args);
        cache.set(key, result);
        return result;
    };
}

// 使用示例
const memoizedFibonacci = memoize(function(n) {
    if (n <= 1) return n;
    return memoizedFibonacci(n - 1) + memoizedFibonacci(n - 2);
});
```

## 最佳实践

1. 函数命名
   ```javascript
   // 使用动词前缀
   function getUserData() { }    // 获取数据
   function setUserData() { }    // 设置数据
   function validateInput() { }  // 验证输入
   function calculateTotal() { } // 计算总额
   ```

2. 参数处理
   ```javascript
   // 参数验证
   function divide(a, b) {
       if (typeof a !== "number" || typeof b !== "number") {
           throw new TypeError("参数必须是数字");
       }
       if (b === 0) {
           throw new Error("除数不能为零");
       }
       return a / b;
   }
   ```

3. 函数组织
   ```javascript
   // 单一职责原则
   // 好的例子
   function validateEmail(email) {
       return /\S+@\S+\.\S+/.test(email);
   }
   
   function sendEmail(email, content) {
       if (!validateEmail(email)) {
           throw new Error("无效的邮箱地址");
       }
       // 发送邮件逻辑
   }
   ```

## 练习

```javascript
// 1. 实现一个compose函数
function compose(...fns) {
    return function(x) {
        return fns.reduceRight((value, fn) => fn(value), x);
    };
}

// 2. 实现一个pipe函数
function pipe(...fns) {
    return function(x) {
        return fns.reduce((value, fn) => fn(value), x);
    };
}

// 使用示例
const addOne = x => x + 1;
const double = x => x * 2;
const square = x => x * x;

const compute = compose(square, double, addOne);
console.log(compute(3)); // ((3 + 1) * 2)² = 64
```

## 总结

- 掌握函数定义的多种方式
- 理解函数参数和返回值
- 掌握作用域和闭包
- 使用高级函数特性
- 遵循最佳实践
- 处理常见应用场景

下一章将介绍JavaScript对象。
