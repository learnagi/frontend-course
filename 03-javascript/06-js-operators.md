---
title: "JavaScript运算符"
slug: "javascript-operators"
sequence: 6
description: "详细介绍JavaScript中的各种运算符及其使用方法"
is_published: true
estimated_minutes: 25
language: "zh-CN"
---

# JavaScript运算符

## 算术运算符

### 1. 基本算术运算符

```javascript
// 加法
let sum = 5 + 3;        // 8
let concat = "Hello" + " World"; // "Hello World"

// 减法
let difference = 10 - 5; // 5

// 乘法
let product = 4 * 3;     // 12

// 除法
let quotient = 15 / 3;   // 5
let decimal = 10 / 3;    // 3.3333...

// 取余（模运算）
let remainder = 17 % 5;  // 2

// 幂运算
let power = 2 ** 3;      // 8（2的3次方）
```

### 2. 自增和自减

```javascript
let x = 5;

// 前置自增
console.log(++x);    // 6（先增加后使用）
console.log(x);      // 6

// 后置自增
let y = 5;
console.log(y++);    // 5（先使用后增加）
console.log(y);      // 6

// 前置自减
let a = 5;
console.log(--a);    // 4（先减少后使用）

// 后置自减
let b = 5;
console.log(b--);    // 5（先使用后减少）
```

## 赋值运算符

### 1. 基本赋值

```javascript
// 简单赋值
let x = 5;

// 链式赋值
let a, b, c;
a = b = c = 5;  // 所有变量都被赋值为5

// 解构赋值
let [first, second] = [1, 2];
let {name, age} = {name: "张三", age: 25};
```

### 2. 复合赋值

```javascript
let num = 10;

// 加法赋值
num += 5;      // 等同于 num = num + 5

// 减法赋值
num -= 3;      // 等同于 num = num - 3

// 乘法赋值
num *= 2;      // 等同于 num = num * 2

// 除法赋值
num /= 4;      // 等同于 num = num / 4

// 取余赋值
num %= 3;      // 等同于 num = num % 3

// 幂运算赋值
num **= 2;     // 等同于 num = num ** 2
```

## 比较运算符

### 1. 相等性比较

```javascript
// 相等和不相等（类型转换）
console.log(5 == "5");     // true
console.log(5 != "5");     // false

// 严格相等和不相等
console.log(5 === "5");    // false
console.log(5 !== "5");    // true

// null和undefined的比较
console.log(null == undefined);   // true
console.log(null === undefined); // false
```

### 2. 大小比较

```javascript
// 大于和小于
console.log(5 > 3);      // true
console.log(5 < 3);      // false

// 大于等于和小于等于
console.log(5 >= 5);     // true
console.log(3 <= 2);     // false

// 字符串比较
console.log("apple" < "banana");  // true（按字母顺序）
console.log("12" > "2");         // false（按字符串比较）
```

## 逻辑运算符

### 1. 基本逻辑运算

```javascript
// 逻辑与 (&&)
console.log(true && true);    // true
console.log(true && false);   // false

// 逻辑或 (||)
console.log(true || false);   // true
console.log(false || false);  // false

// 逻辑非 (!)
console.log(!true);           // false
console.log(!false);          // true
```

### 2. 短路求值

```javascript
// 逻辑与的短路
console.log(false && anything);  // false（不会执行anything）

// 逻辑或的短路
console.log(true || anything);   // true（不会执行anything）

// 实际应用
let user = null;
let name = user && user.name;    // null（安全访问属性）

let defaultName = "游客";
let displayName = user || defaultName;  // "游客"（设置默认值）
```

## 条件（三元）运算符

```javascript
// 基本用法
let age = 20;
let status = age >= 18 ? "成年" : "未成年";

// 嵌套使用
let score = 75;
let result = score >= 90 ? "优秀" :
             score >= 60 ? "及格" :
             "不及格";

// 与空值合并
let user = {
    name: "张三",
    age: null
};
let displayAge = user.age ?? "未知年龄";
```

## 位运算符

```javascript
// 按位与 (&)
console.log(5 & 3);   // 1

// 按位或 (|)
console.log(5 | 3);   // 7

// 按位异或 (^)
console.log(5 ^ 3);   // 6

// 按位非 (~)
console.log(~5);      // -6

// 左移 (<<)
console.log(5 << 1);  // 10

// 右移 (>>)
console.log(5 >> 1);  // 2

// 无符号右移 (>>>)
console.log(-5 >>> 1); // 2147483645
```

## 特殊运算符

### 1. typeof运算符

```javascript
console.log(typeof 42);           // "number"
console.log(typeof "hello");      // "string"
console.log(typeof true);         // "boolean"
console.log(typeof undefined);    // "undefined"
console.log(typeof null);         // "object"（这是一个历史遗留bug）
console.log(typeof {});           // "object"
console.log(typeof []);           // "object"
console.log(typeof function(){}); // "function"
```

### 2. instanceof运算符

```javascript
let arr = [];
let obj = {};
class Person {}
let person = new Person();

console.log(arr instanceof Array);    // true
console.log(obj instanceof Object);   // true
console.log(person instanceof Person);// true
```

## 运算符优先级

```javascript
// 优先级示例
let result = 2 + 3 * 4;    // 14（乘法优先）
let result2 = (2 + 3) * 4; // 20（括号优先）

// 复杂表达式
let x = 5;
let y = 3;
let z = 2;
let result3 = x + y * z++;  // 11（先乘法，后自增）
```

## 最佳实践

1. 使用严格相等
   ```javascript
   // 推荐
   if (value === null) {}
   
   // 不推荐
   if (value == null) {}
   ```

2. 使用简洁的赋值
   ```javascript
   // 推荐
   x += 5;
   
   // 不推荐
   x = x + 5;
   ```

3. 使用括号提高可读性
   ```javascript
   // 推荐
   let result = (a + b) * c;
   
   // 不推荐
   let result = a + b * c;
   ```

## 练习

```javascript
// 1. 实现一个简单的计算器
function calculate(a, b, operator) {
    switch (operator) {
        case '+': return a + b;
        case '-': return a - b;
        case '*': return a * b;
        case '/': return b !== 0 ? a / b : "除数不能为零";
        default: return "无效的运算符";
    }
}

// 2. 实现安全的属性访问
function safeGet(obj, path) {
    return path.split('.').reduce((acc, key) => 
        acc && acc[key], obj) ?? undefined;
}
```

## 总结

- 掌握各类运算符的使用
- 理解运算符优先级
- 使用短路求值优化代码
- 注意类型转换的影响
- 遵循最佳实践

下一章将介绍JavaScript的数据类型。
