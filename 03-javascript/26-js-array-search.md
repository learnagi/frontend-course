---
title: "JavaScript数组搜索"
slug: "javascript-array-search"
sequence: 26
description: "详细介绍JavaScript数组的搜索方法及其使用场景"
---

# JavaScript数组搜索

在JavaScript中，数组提供了多种搜索方法，可以帮助我们快速找到所需的元素。本章将详细介绍这些方法的使用和最佳实践。

## 基础搜索方法

### 1. indexOf 和 lastIndexOf

```javascript
const numbers = [1, 2, 3, 2, 1];

// indexOf - 从前向后查找元素的索引
console.log(numbers.indexOf(2));        // 1
console.log(numbers.indexOf(4));        // -1

// lastIndexOf - 从后向前查找元素的索引
console.log(numbers.lastIndexOf(2));    // 3
console.log(numbers.lastIndexOf(4));    // -1

// 指定起始位置查找
console.log(numbers.indexOf(2, 2));     // 3
console.log(numbers.lastIndexOf(2, 2)); // 1
```

### 2. includes 方法

```javascript
const fruits = ['apple', 'banana', 'orange'];

// 检查数组是否包含某个元素
console.log(fruits.includes('banana'));     // true
console.log(fruits.includes('grape'));      // false

// 从指定位置开始检查
console.log(fruits.includes('apple', 1));   // false
```

## 高级搜索方法

### 1. find 和 findIndex

```javascript
const users = [
    { id: 1, name: 'Alice', age: 25 },
    { id: 2, name: 'Bob', age: 30 },
    { id: 3, name: 'Charlie', age: 35 }
];

// find - 查找满足条件的第一个元素
const user = users.find(user => user.age > 28);
console.log(user);  // { id: 2, name: 'Bob', age: 30 }

// findIndex - 查找满足条件的第一个元素的索引
const index = users.findIndex(user => user.age > 28);
console.log(index); // 1

// 未找到时的返回值
const notFound = users.find(user => user.age > 40);
console.log(notFound);                  // undefined
console.log(users.findIndex(user => user.age > 40));  // -1
```

### 2. findLast 和 findLastIndex

```javascript
// findLast - 从后向前查找满足条件的第一个元素
const lastUser = users.findLast(user => user.age > 28);
console.log(lastUser);  // { id: 3, name: 'Charlie', age: 35 }

// findLastIndex - 从后向前查找满足条件的第一个元素的索引
const lastIndex = users.findLastIndex(user => user.age > 28);
console.log(lastIndex); // 2
```

## 实践应用

### 1. 复杂对象搜索

```javascript
const products = [
    { id: 1, name: 'iPhone', category: 'Electronics', price: 999 },
    { id: 2, name: 'MacBook', category: 'Electronics', price: 1299 },
    { id: 3, name: 'Coffee Maker', category: 'Appliances', price: 79 }
];

// 按多个条件搜索
const findProduct = (products, criteria) => {
    return products.find(product => {
        return Object.entries(criteria).every(([key, value]) => 
            product[key] === value
        );
    });
};

// 使用示例
const result = findProduct(products, { 
    category: 'Electronics',
    price: 999
});
console.log(result); // { id: 1, name: 'iPhone', ... }
```

### 2. 模糊搜索

```javascript
// 实现简单的模糊搜索
const fuzzySearch = (array, searchTerm) => {
    const term = searchTerm.toLowerCase();
    return array.filter(item => 
        item.name.toLowerCase().includes(term)
    );
};

// 使用示例
const searchResults = fuzzySearch(products, 'phone');
console.log(searchResults); // [{ id: 1, name: 'iPhone', ... }]
```

## 最佳实践

1. 选择合适的搜索方法
   ```javascript
   // 简单值查找用includes
   if (array.includes(value)) { ... }
   
   // 需要索引用indexOf/lastIndexOf
   const index = array.indexOf(value);
   
   // 对象查找用find/findIndex
   const item = array.find(predicate);
   ```

2. 性能优化
   ```javascript
   // 避免重复搜索
   const index = array.indexOf(value);
   if (index !== -1) {
       const item = array[index];
       // 使用item...
   }
   
   // 大数组考虑使用Set
   const set = new Set(array);
   if (set.has(value)) { ... }
   ```

3. 错误处理
   ```javascript
   // 处理未找到的情况
   const found = array.find(predicate) ?? defaultValue;
   
   // 索引检查
   const index = array.findIndex(predicate);
   if (index !== -1) {
       // 安全地使用索引
   }
   ```

## 总结

- 掌握基础搜索方法（indexOf、includes）
- 熟练使用高级搜索方法（find、findIndex）
- 了解从后向前搜索的方法（findLast、findLastIndex）
- 实现自定义搜索功能
- 注意性能优化和错误处理
- 选择合适的搜索方法

下一章将介绍JavaScript数组的排序方法。
