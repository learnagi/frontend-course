---
title: "JavaScript赋值运算"
slug: "javascript-assignment"
sequence: 8
description: "详细介绍JavaScript中的赋值运算和赋值运算符"
is_published: true
estimated_minutes: 20
language: "zh-CN"
---

# JavaScript赋值运算

## 基本赋值

### 1. 简单赋值

```javascript
// 基本赋值运算符
let x = 5;
let name = "张三";
let isActive = true;

// 多重赋值
let a, b, c;
a = b = c = 0;  // 所有变量都被赋值为0

// undefined赋值
let undefinedVar;  // 自动赋值为undefined
```

### 2. 解构赋值

```javascript
// 数组解构
let [first, second] = [1, 2];
let [one, , three] = [1, 2, 3];  // 跳过元素

// 对象解构
let {name, age} = {name: "张三", age: 25};
let {title: jobTitle} = {title: "工程师"};  // 重命名

// 默认值
let [x = 1] = [];  // x = 1
let {y = 2} = {};  // y = 2

// 嵌套解构
let {
    info: {
        address,
        phone = "未知"
    } = {}
} = {info: {address: "北京"}};
```

## 复合赋值

### 1. 算术复合赋值

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

### 2. 位运算复合赋值

```javascript
let bits = 5;  // 二进制：101

// 按位与赋值
bits &= 3;     // 等同于 bits = bits & 3

// 按位或赋值
bits |= 8;     // 等同于 bits = bits | 8

// 按位异或赋值
bits ^= 2;     // 等同于 bits = bits ^ 2

// 左移赋值
bits <<= 1;    // 等同于 bits = bits << 1

// 右移赋值
bits >>= 1;    // 等同于 bits = bits >> 1

// 无符号右移赋值
bits >>>= 1;   // 等同于 bits = bits >>> 1
```

## 逻辑赋值

### 1. 逻辑运算符赋值

```javascript
// 逻辑与赋值
let a = true;
a &&= false;   // 等同于 a = a && false

// 逻辑或赋值
let b = false;
b ||= true;    // 等同于 b = b || true

// 空值合并赋值
let c = null;
c ??= "默认值"; // 等同于 c = c ?? "默认值"
```

### 2. 实际应用

```javascript
// 对象属性的默认值
function updateUser(user) {
    // 只在user.name为空时设置默认值
    user.name ||= "匿名用户";
    
    // 只在user.age为null或undefined时设置默认值
    user.age ??= 0;
    
    // 只在user.isActive为true时更新状态
    user.status &&= "活跃";
    
    return user;
}
```

## 链式赋值

### 1. 基本链式赋值

```javascript
// 多个变量赋相同的值
let x, y, z;
x = y = z = 0;

// 函数返回值赋值
function setValue() {
    return 42;
}
let a, b;
a = b = setValue();
```

### 2. 解构链式赋值

```javascript
// 数组解构链式赋值
let arr = [1, 2, 3];
let [a, b] = arr;
[b, a] = [a, b];  // 交换值

// 对象解构链式赋值
let obj = { x: 1, y: 2 };
let { x: first, y: second } = obj;
({ x: second, y: first } = obj);
```

## 特殊赋值情况

### 1. 类型转换

```javascript
// 数字转字符串
let num = 42;
num += "";     // "42"

// 字符串转数字
let str = "42";
str -= 0;      // 42

// 布尔值转换
let bool = 1;
bool &&= true;  // true
```

### 2. 属性赋值

```javascript
// 动态属性名赋值
let propertyName = "color";
let obj = {};
obj[propertyName] = "red";

// 计算属性名
let prefix = "user";
let userData = {
    [`${prefix}Name`]: "张三",
    [`${prefix}Age`]: 25
};
```

## 最佳实践

### 1. 代码简洁性

```javascript
// 推荐的写法
let count = 0;
count += 1;

// 不推荐的写法
let count = 0;
count = count + 1;

// 使用解构简化代码
const { name, age } = user;
// 替代
// const name = user.name;
// const age = user.age;
```

### 2. 安全赋值

```javascript
// 使用空值合并运算符
function createUser(data) {
    return {
        name: data?.name ?? "匿名用户",
        age: data?.age ?? 0,
        settings: data?.settings ?? {}
    };
}

// 防止意外覆盖
const config = Object.freeze({
    apiUrl: "https://api.example.com",
    timeout: 5000
});
```

## 练习

```javascript
// 1. 实现深度赋值
function deepAssign(target, source) {
    for (let key in source) {
        if (source.hasOwnProperty(key)) {
            if (typeof source[key] === 'object' && source[key] !== null) {
                target[key] = deepAssign(target[key] ?? {}, source[key]);
            } else {
                target[key] = source[key];
            }
        }
    }
    return target;
}

// 2. 创建对象属性代理
function createProxy(obj, defaultValue) {
    return new Proxy(obj, {
        get(target, property) {
            target[property] ??= defaultValue;
            return target[property];
        }
    });
}

// 使用示例
const user = createProxy({}, "未设置");
console.log(user.name);  // "未设置"
```

## 总结

- 掌握基本赋值运算
- 理解复合赋值运算符
- 使用解构赋值简化代码
- 注意类型转换
- 遵循最佳实践
- 处理特殊赋值情况

下一章将介绍JavaScript的数据类型。
