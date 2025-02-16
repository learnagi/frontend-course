---
title: "JavaScript数组排序"
slug: "javascript-array-sort"
sequence: 27
description: "详细介绍JavaScript数组的排序方法及其应用场景"
---

# JavaScript数组排序

JavaScript提供了强大的数组排序功能，本章将详细介绍数组排序的各种方法和技巧。

## 基础排序

### 1. sort方法

```javascript
// 默认排序（按字符串顺序）
const fruits = ['banana', 'apple', 'orange'];
fruits.sort();
console.log(fruits);  // ['apple', 'banana', 'orange']

// 数字排序
const numbers = [10, 2, 5, 1, 9];
numbers.sort((a, b) => a - b);  // 升序
console.log(numbers);  // [1, 2, 5, 9, 10]

numbers.sort((a, b) => b - a);  // 降序
console.log(numbers);  // [10, 9, 5, 2, 1]
```

### 2. reverse方法

```javascript
const arr = [1, 2, 3, 4, 5];
arr.reverse();
console.log(arr);  // [5, 4, 3, 2, 1]

// 链式调用
const descendingArr = [1, 2, 3, 4, 5].sort((a, b) => b - a);
console.log(descendingArr);  // [5, 4, 3, 2, 1]
```

## 高级排序

### 1. 对象数组排序

```javascript
const users = [
    { name: 'Alice', age: 25, score: 85 },
    { name: 'Bob', age: 30, score: 92 },
    { name: 'Charlie', age: 28, score: 88 }
];

// 按年龄排序
users.sort((a, b) => a.age - b.age);

// 按名字排序（使用localeCompare）
users.sort((a, b) => a.name.localeCompare(b.name));

// 按多个条件排序
users.sort((a, b) => {
    if (a.score !== b.score) {
        return b.score - a.score;  // 首先按分数降序
    }
    return a.age - b.age;  // 分数相同时按年龄升序
});
```

### 2. 自定义排序规则

```javascript
// 自定义排序函数
const customSort = (arr, getCompareValue) => {
    return arr.sort((a, b) => {
        const valueA = getCompareValue(a);
        const valueB = getCompareValue(b);
        return valueA < valueB ? -1 : valueA > valueB ? 1 : 0;
    });
};

// 使用示例
const data = [
    { id: 1, priority: 'high' },
    { id: 2, priority: 'low' },
    { id: 3, priority: 'medium' }
];

const priorityOrder = { low: 1, medium: 2, high: 3 };
customSort(data, item => priorityOrder[item.priority]);
```

## 实践应用

### 1. 表格数据排序

```javascript
const tableData = [
    { id: 1, name: 'Product A', price: 99.99, stock: 50 },
    { id: 2, name: 'Product B', price: 149.99, stock: 30 },
    { id: 3, name: 'Product C', price: 79.99, stock: 100 }
];

// 通用排序函数
const sortTable = (data, field, ascending = true) => {
    return [...data].sort((a, b) => {
        let comparison = 0;
        
        // 处理不同类型的值
        if (typeof a[field] === 'string') {
            comparison = a[field].localeCompare(b[field]);
        } else {
            comparison = a[field] - b[field];
        }
        
        return ascending ? comparison : -comparison;
    });
};

// 使用示例
console.log(sortTable(tableData, 'price', false));  // 按价格降序
console.log(sortTable(tableData, 'name', true));    // 按名称升序
```

### 2. 稳定排序

```javascript
// 实现稳定排序
const stableSort = (arr, compare) => {
    return arr
        .map((item, index) => ({ item, index }))
        .sort((a, b) => {
            const order = compare(a.item, b.item);
            return order !== 0 ? order : a.index - b.index;
        })
        .map(({ item }) => item);
};

// 使用示例
const items = [
    { category: 'A', value: 1 },
    { category: 'B', value: 1 },
    { category: 'A', value: 2 }
];

const sorted = stableSort(items, (a, b) => a.value - b.value);
```

## 性能优化

### 1. 大数据集排序

```javascript
// 分块排序
const chunkSort = (arr, chunkSize = 1000) => {
    const chunks = [];
    for (let i = 0; i < arr.length; i += chunkSize) {
        chunks.push(arr.slice(i, i + chunkSize));
    }
    
    // 对每个块进行排序
    const sortedChunks = chunks.map(chunk => 
        chunk.sort((a, b) => a - b)
    );
    
    // 合并排序后的块
    return sortedChunks.reduce((merged, chunk) => {
        const result = [];
        let i = 0, j = 0;
        
        while (i < merged.length && j < chunk.length) {
            result.push(
                merged[i] <= chunk[j] ? merged[i++] : chunk[j++]
            );
        }
        
        return result.concat(merged.slice(i), chunk.slice(j));
    });
};
```

## 最佳实践

1. 排序方法选择
   ```javascript
   // 简单数据类型使用基础排序
   array.sort((a, b) => a - b);
   
   // 字符串使用localeCompare
   array.sort((a, b) => a.localeCompare(b));
   
   // 复杂对象使用自定义排序
   array.sort((a, b) => compareFunction(a, b));
   ```

2. 性能考虑
   ```javascript
   // 避免在排序函数中重复计算
   const sortByComputedValue = (arr) => {
       const cached = arr.map(item => ({
           original: item,
           computed: expensiveComputation(item)
       }));
       
       cached.sort((a, b) => a.computed - b.computed);
       return cached.map(item => item.original);
   };
   ```

3. 错误处理
   ```javascript
   // 安全的排序函数
   const safeSortNumbers = (arr) => {
       return arr.sort((a, b) => {
           if (typeof a !== 'number' || typeof b !== 'number') {
               return 0;  // 保持原有顺序
           }
           return a - b;
       });
   };
   ```

## 总结

- 掌握基础排序方法（sort、reverse）
- 理解自定义排序规则
- 熟练处理对象数组排序
- 实现高级排序功能
- 注意性能优化
- 遵循最佳实践

下一章将介绍JavaScript数组的高级操作方法。
