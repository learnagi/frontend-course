---
title: "JavaScript数组和对象"
slug: "javascript-arrays-objects"
sequence: 5
description: "掌握JavaScript中数组和对象的操作方法及最佳实践"
is_published: true
estimated_minutes: 40
language: "zh-CN"
---

# JavaScript数组和对象

## 数组基础

### 1. 数组创建和访问

```javascript
// 创建数组
let fruits = ["apple", "banana", "orange"];
let numbers = new Array(1, 2, 3);
let empty = new Array(3); // 创建长度为3的空数组

// 访问元素
console.log(fruits[0]);     // "apple"
console.log(fruits.at(-1)); // "orange"（从末尾访问）

// 数组长度
console.log(fruits.length); // 3

// 修改数组
fruits[1] = "grape";
fruits.length = 2; // 通过修改length裁剪数组
```

### 2. 数组方法

```javascript
// 添加和删除元素
let arr = ["a", "b", "c"];

// 末尾操作
arr.push("d");     // 添加到末尾
arr.pop();         // 从末尾删除

// 开头操作
arr.unshift("x");  // 添加到开头
arr.shift();       // 从开头删除

// 中间操作
arr.splice(1, 1);          // 删除元素
arr.splice(1, 0, "new");   // 插入元素
arr.splice(1, 1, "new");   // 替换元素

// 数组切片
let sliced = arr.slice(1, 3);  // 提取部分数组
let copied = arr.slice();      // 复制整个数组
```

### 3. 数组遍历

```javascript
let numbers = [1, 2, 3, 4, 5];

// for循环
for (let i = 0; i < numbers.length; i++) {
    console.log(numbers[i]);
}

// for...of循环
for (let num of numbers) {
    console.log(num);
}

// forEach方法
numbers.forEach((num, index) => {
    console.log(`索引${index}: ${num}`);
});

// map方法
let doubled = numbers.map(num => num * 2);

// filter方法
let evenNumbers = numbers.filter(num => num % 2 === 0);

// reduce方法
let sum = numbers.reduce((total, num) => total + num, 0);

// some和every方法
let hasEven = numbers.some(num => num % 2 === 0);
let allPositive = numbers.every(num => num > 0);
```

### 4. 数组排序

```javascript
let fruits = ["banana", "apple", "orange"];
let numbers = [4, 2, 5, 1, 3];

// 基本排序
fruits.sort();                     // 字母顺序
numbers.sort((a, b) => a - b);    // 数字升序
numbers.sort((a, b) => b - a);    // 数字降序

// 自定义排序
let users = [
    { name: "John", age: 30 },
    { name: "Jane", age: 25 },
    { name: "Bob", age: 35 }
];

users.sort((a, b) => a.age - b.age); // 按年龄排序
```

## 对象基础

### 1. 对象创建和访问

```javascript
// 对象字面量
let person = {
    name: "John",
    age: 30,
    "like-sports": true  // 特殊属性名
};

// 访问属性
console.log(person.name);          // 点号访问
console.log(person["age"]);        // 方括号访问
console.log(person["like-sports"]); // 必须使用方括号

// 动态属性
let propertyName = "age";
console.log(person[propertyName]); // 30

// 属性存在性检查
console.log("name" in person);           // true
console.log(person.hasOwnProperty("age")); // true
```

### 2. 对象方法

```javascript
let calculator = {
    // 方法简写
    add(a, b) {
        return a + b;
    },
    
    // 传统方法定义
    multiply: function(a, b) {
        return a * b;
    },
    
    // 箭头函数（注意this绑定）
    subtract: (a, b) => a - b
};

// 使用方法
console.log(calculator.add(5, 3));      // 8
console.log(calculator.multiply(4, 2));  // 8
```

### 3. 对象遍历

```javascript
let user = {
    name: "John",
    age: 30,
    city: "New York"
};

// for...in循环
for (let key in user) {
    console.log(`${key}: ${user[key]}`);
}

// Object.keys()
Object.keys(user).forEach(key => {
    console.log(`${key}: ${user[key]}`);
});

// Object.values()
Object.values(user).forEach(value => {
    console.log(value);
});

// Object.entries()
Object.entries(user).forEach(([key, value]) => {
    console.log(`${key}: ${value}`);
});
```

## 高级特性

### 1. 解构赋值

```javascript
// 数组解构
let [a, b, ...rest] = [1, 2, 3, 4, 5];
console.log(a, b, rest); // 1, 2, [3, 4, 5]

// 对象解构
let { name, age, city = "Unknown" } = user;
console.log(name, age, city);

// 嵌套解构
let options = {
    size: {
        width: 100,
        height: 200
    },
    items: ["Cake", "Donut"],
    extra: true
};

let {
    size: { width, height },
    items: [item1, item2],
    extra
} = options;
```

### 2. 展开运算符

```javascript
// 数组展开
let arr1 = [1, 2, 3];
let arr2 = [4, 5, 6];
let combined = [...arr1, ...arr2];

// 对象展开
let defaults = { theme: "light", fontSize: 12 };
let userPreferences = { fontSize: 14 };
let settings = { ...defaults, ...userPreferences };
```

### 3. 对象方法和属性

```javascript
// 对象属性描述符
let person = {};

Object.defineProperty(person, "name", {
    value: "John",
    writable: false,     // 是否可修改
    enumerable: true,    // 是否可枚举
    configurable: false  // 是否可配置
});

// 访问器属性
let user = {
    firstName: "John",
    lastName: "Doe",
    
    get fullName() {
        return `${this.firstName} ${this.lastName}`;
    },
    
    set fullName(value) {
        [this.firstName, this.lastName] = value.split(" ");
    }
};

console.log(user.fullName);    // "John Doe"
user.fullName = "Jane Smith";
```

## 实践示例

### 1. 深拷贝函数

```javascript
function deepClone(obj) {
    if (obj === null || typeof obj !== "object") {
        return obj;
    }
    
    if (Array.isArray(obj)) {
        return obj.map(item => deepClone(item));
    }
    
    return Object.fromEntries(
        Object.entries(obj).map(([key, value]) => [key, deepClone(value)])
    );
}

// 使用示例
let original = {
    name: "John",
    settings: {
        theme: "dark",
        notifications: true
    },
    items: [1, 2, { id: 1 }]
};

let cloned = deepClone(original);
```

### 2. 数组去重和扁平化

```javascript
// 数组去重
function unique(arr) {
    return [...new Set(arr)];
}

// 数组扁平化
function flatten(arr) {
    return arr.reduce((flat, item) => {
        return flat.concat(Array.isArray(item) ? flatten(item) : item);
    }, []);
}

// 使用示例
let numbers = [1, 2, 2, 3, [4, 5, [6, 7]], 8];
console.log(unique([1, 2, 2, 3, 3, 4]));    // [1, 2, 3, 4]
console.log(flatten(numbers));               // [1, 2, 3, 4, 5, 6, 7, 8]
```

## 最佳实践

1. 数组操作
   - 使用不可变方法（map, filter, reduce）而不是修改原数组
   - 使用Array.isArray()检查数组类型
   - 避免在循环中修改数组长度

2. 对象操作
   - 使用对象字面量创建对象
   - 使用计算属性名动态设置属性
   - 使用Object.freeze()防止对象被修改

3. 性能考虑
   - 避免频繁修改数组长度
   - 使用适当的遍历方法
   - 注意深拷贝的性能开销

## 练习

```javascript
// 1. 实现数组分组
function groupBy(array, key) {
    return array.reduce((grouped, item) => {
        const value = typeof key === "function" ? key(item) : item[key];
        return {
            ...grouped,
            [value]: [...(grouped[value] || []), item]
        };
    }, {});
}

// 2. 实现对象合并
function mergeDeep(target, ...sources) {
    if (!sources.length) return target;
    const source = sources.shift();

    if (isObject(target) && isObject(source)) {
        for (const key in source) {
            if (isObject(source[key])) {
                if (!target[key]) Object.assign(target, { [key]: {} });
                mergeDeep(target[key], source[key]);
            } else {
                Object.assign(target, { [key]: source[key] });
            }
        }
    }

    return mergeDeep(target, ...sources);
}

function isObject(item) {
    return item && typeof item === "object" && !Array.isArray(item);
}
```

## 总结

- 掌握数组和对象的基本操作
- 理解并使用高级特性
- 注意性能和最佳实践
- 使用适当的工具函数
- 保持代码的可维护性

下一章将介绍JavaScript的异步编程。
