---
title: "JavaScript数组"
slug: "javascript-arrays"
sequence: 24
description: "详细介绍JavaScript数组的基础知识和使用方法"
is_published: true
estimated_minutes: 25
language: "zh-CN"
---

# JavaScript数组

## 数组基础

### 1. 创建数组

```javascript
// 字面量创建
const arr1 = [1, 2, 3, 4, 5];
const arr2 = ['apple', 'banana', 'orange'];
const arr3 = [1, 'hello', { name: 'John' }, [1, 2, 3]];

// Array构造函数
const arr4 = new Array(3);           // 创建长度为3的空数组
const arr5 = new Array(1, 2, 3);     // 创建包含1,2,3的数组

// Array.from
const arr6 = Array.from('hello');    // ['h', 'e', 'l', 'l', 'o']
const arr7 = Array.from([1, 2, 3], x => x * 2); // [2, 4, 6]

// Array.of
const arr8 = Array.of(3);            // [3]
const arr9 = Array.of(1, 2, 3);      // [1, 2, 3]
```

### 2. 访问数组

```javascript
const fruits = ['apple', 'banana', 'orange'];

// 索引访问
console.log(fruits[0]);              // 'apple'
console.log(fruits[fruits.length-1]); // 'orange'

// 解构赋值
const [first, second] = fruits;
console.log(first, second);          // 'apple' 'banana'

// 扩展运算符
const moreFruits = [...fruits, 'grape'];
console.log(moreFruits);             // ['apple', 'banana', 'orange', 'grape']

// 数组长度
console.log(fruits.length);          // 3
```

## 数组操作

### 1. 添加和删除元素

```javascript
const arr = ['a', 'b', 'c'];

// 末尾添加
arr.push('d');                // ['a', 'b', 'c', 'd']

// 开头添加
arr.unshift('x');            // ['x', 'a', 'b', 'c', 'd']

// 末尾删除
const last = arr.pop();      // ['x', 'a', 'b', 'c']

// 开头删除
const first = arr.shift();   // ['a', 'b', 'c']

// 中间操作
arr.splice(1, 1);            // ['a', 'c']
arr.splice(1, 0, 'b');       // ['a', 'b', 'c']
```

### 2. 数组合并和分割

```javascript
const arr1 = [1, 2];
const arr2 = [3, 4];

// 合并数组
const combined1 = arr1.concat(arr2);        // [1, 2, 3, 4]
const combined2 = [...arr1, ...arr2];       // [1, 2, 3, 4]

// 分割数组
const numbers = [1, 2, 3, 4, 5];
const slice1 = numbers.slice(1, 3);         // [2, 3]
const slice2 = numbers.slice(-2);           // [4, 5]

// 分割字符串为数组
const str = 'hello,world';
const parts = str.split(',');               // ['hello', 'world']
```

## 数组遍历

### 1. 循环遍历

```javascript
const arr = ['a', 'b', 'c'];

// for循环
for (let i = 0; i < arr.length; i++) {
    console.log(arr[i]);
}

// for...of循环
for (const item of arr) {
    console.log(item);
}

// forEach方法
arr.forEach((item, index) => {
    console.log(item, index);
});

// for...in循环（不推荐用于数组）
for (const index in arr) {
    console.log(arr[index]);
}
```

### 2. 迭代器方法

```javascript
const numbers = [1, 2, 3, 4, 5];

// map - 映射
const doubled = numbers.map(x => x * 2);
console.log(doubled);  // [2, 4, 6, 8, 10]

// filter - 过滤
const evens = numbers.filter(x => x % 2 === 0);
console.log(evens);   // [2, 4]

// reduce - 归约
const sum = numbers.reduce((acc, cur) => acc + cur, 0);
console.log(sum);     // 15

// some - 是否存在满足条件的元素
const hasEven = numbers.some(x => x % 2 === 0);
console.log(hasEven); // true

// every - 是否所有元素都满足条件
const allPositive = numbers.every(x => x > 0);
console.log(allPositive); // true
```

## 数组排序

### 1. 基本排序

```javascript
const numbers = [3, 1, 4, 1, 5, 9, 2, 6, 5, 3, 5];

// 默认排序（按字符串排序）
numbers.sort();

// 数字排序
numbers.sort((a, b) => a - b);  // 升序
numbers.sort((a, b) => b - a);  // 降序

// 字符串排序
const fruits = ['banana', 'apple', 'orange'];
fruits.sort();  // ['apple', 'banana', 'orange']

// 自定义排序
const items = [
    { name: 'Edward', value: 21 },
    { name: 'Sharpe', value: 37 },
    { name: 'And', value: 45 }
];

items.sort((a, b) => a.value - b.value);  // 按value排序
items.sort((a, b) => a.name.localeCompare(b.name));  // 按name排序
```

### 2. 高级排序

```javascript
class ArraySorter {
    // 快速排序
    static quickSort(arr) {
        if (arr.length <= 1) return arr;
        
        const pivot = arr[0];
        const left = [];
        const right = [];
        
        for (let i = 1; i < arr.length; i++) {
            if (arr[i] < pivot) {
                left.push(arr[i]);
            } else {
                right.push(arr[i]);
            }
        }
        
        return [...this.quickSort(left), pivot, ...this.quickSort(right)];
    }
    
    // 归并排序
    static mergeSort(arr) {
        if (arr.length <= 1) return arr;
        
        const mid = Math.floor(arr.length / 2);
        const left = arr.slice(0, mid);
        const right = arr.slice(mid);
        
        return this.merge(
            this.mergeSort(left),
            this.mergeSort(right)
        );
    }
    
    static merge(left, right) {
        const result = [];
        let leftIndex = 0;
        let rightIndex = 0;
        
        while (leftIndex < left.length && rightIndex < right.length) {
            if (left[leftIndex] < right[rightIndex]) {
                result.push(left[leftIndex]);
                leftIndex++;
            } else {
                result.push(right[rightIndex]);
                rightIndex++;
            }
        }
        
        return result
            .concat(left.slice(leftIndex))
            .concat(right.slice(rightIndex));
    }
}
```

## 数组检索

### 1. 查找元素

```javascript
const numbers = [1, 2, 3, 4, 5, 2];

// indexOf - 查找元素索引
console.log(numbers.indexOf(2));        // 1
console.log(numbers.lastIndexOf(2));    // 5

// includes - 检查是否包含元素
console.log(numbers.includes(3));       // true
console.log(numbers.includes(6));       // false

// find - 查找满足条件的第一个元素
const found = numbers.find(x => x > 3);
console.log(found);                     // 4

// findIndex - 查找满足条件的第一个元素的索引
const foundIndex = numbers.findIndex(x => x > 3);
console.log(foundIndex);                // 3
```

### 2. 高级查找

```javascript
class ArrayFinder {
    // 二分查找（要求数组已排序）
    static binarySearch(arr, target) {
        let left = 0;
        let right = arr.length - 1;
        
        while (left <= right) {
            const mid = Math.floor((left + right) / 2);
            
            if (arr[mid] === target) {
                return mid;
            } else if (arr[mid] < target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        
        return -1;
    }
    
    // 查找所有匹配项
    static findAll(arr, predicate) {
        return arr.reduce((matches, item, index) => {
            if (predicate(item)) {
                matches.push({ item, index });
            }
            return matches;
        }, []);
    }
    
    // 模糊查找
    static fuzzySearch(arr, query) {
        const lowercaseQuery = query.toLowerCase();
        return arr.filter(item => 
            String(item).toLowerCase().includes(lowercaseQuery)
        );
    }
}
```

## 数组转换

### 1. 类型转换

```javascript
// 数组转字符串
const arr = [1, 2, 3, 4, 5];
console.log(arr.toString());        // "1,2,3,4,5"
console.log(arr.join('-'));         // "1-2-3-4-5"

// 字符串转数组
const str = '1,2,3,4,5';
console.log(str.split(','));        // [1, 2, 3, 4, 5]

// 类数组对象转数组
function example() {
    const args = Array.from(arguments);
    console.log(args);
}

// Set转数组
const set = new Set([1, 2, 3]);
const arrFromSet = Array.from(set);
// 或者
const arrFromSet2 = [...set];

// Map转数组
const map = new Map([['a', 1], ['b', 2]]);
const arrFromMap = Array.from(map);
```

### 2. 数据转换

```javascript
class ArrayTransformer {
    // 扁平化数组
    static flatten(arr, depth = 1) {
        return arr.flat(depth);
    }
    
    // 去重
    static unique(arr) {
        return [...new Set(arr)];
    }
    
    // 分组
    static groupBy(arr, key) {
        return arr.reduce((groups, item) => {
            const group = (typeof key === 'function') ? key(item) : item[key];
            groups[group] = groups[group] || [];
            groups[group].push(item);
            return groups;
        }, {});
    }
    
    // 转换为树形结构
    static toTree(arr, idKey = 'id', parentKey = 'parentId', childrenKey = 'children') {
        const map = {};
        const roots = [];
        
        // 创建节点映射
        arr.forEach(item => {
            map[item[idKey]] = { ...item, [childrenKey]: [] };
        });
        
        // 构建树形结构
        arr.forEach(item => {
            const node = map[item[idKey]];
            if (item[parentKey]) {
                const parent = map[item[parentKey]];
                if (parent) {
                    parent[childrenKey].push(node);
                }
            } else {
                roots.push(node);
            }
        });
        
        return roots;
    }
}
```

## 最佳实践

1. 数组创建
   ```javascript
   // 推荐：使用字面量创建
   const arr = [1, 2, 3];
   
   // 推荐：使用Array.from转换可迭代对象
   const arrFromSet = Array.from(new Set([1, 2, 3]));
   ```

2. 数组复制
   ```javascript
   // 推荐：使用扩展运算符
   const original = [1, 2, 3];
   const copy = [...original];
   
   // 推荐：使用slice
   const copy2 = original.slice();
   ```

3. 性能优化
   ```javascript
   // 推荐：预分配数组大小
   const arr = new Array(1000);
   
   // 推荐：使用适当的迭代方法
   // forEach适用于简单迭代
   // map适用于转换
   // reduce适用于归约
   // filter适用于过滤
   ```

## 总结

- 掌握数组基础
- 熟练数组操作
- 使用数组方法
- 实现数组排序
- 处理数组检索
- 应用最佳实践

下一章将介绍JavaScript数组方法。
