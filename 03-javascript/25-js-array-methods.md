---
title: "JavaScript数组方法"
slug: "javascript-array-methods"
sequence: 25
description: "详细介绍JavaScript数组的各种方法及其使用"
is_published: true
estimated_minutes: 25
language: "zh-CN"
---

# JavaScript数组方法

## 修改数组的方法

### 1. 添加和删除元素

```javascript
const arr = ['a', 'b', 'c'];

// push - 末尾添加元素
arr.push('d', 'e');              // 返回新长度 5
console.log(arr);                // ['a', 'b', 'c', 'd', 'e']

// unshift - 开头添加元素
arr.unshift('x', 'y');          // 返回新长度 7
console.log(arr);                // ['x', 'y', 'a', 'b', 'c', 'd', 'e']

// pop - 删除最后一个元素
const last = arr.pop();          // 返回被删除的元素 'e'
console.log(arr);                // ['x', 'y', 'a', 'b', 'c', 'd']

// shift - 删除第一个元素
const first = arr.shift();       // 返回被删除的元素 'x'
console.log(arr);                // ['y', 'a', 'b', 'c', 'd']
```

### 2. 修改数组内容

```javascript
const arr = ['a', 'b', 'c', 'd', 'e'];

// splice - 删除或替换元素
arr.splice(1, 2);               // 从索引1开始删除2个元素
console.log(arr);               // ['a', 'd', 'e']

arr.splice(1, 0, 'b', 'c');    // 在索引1处插入元素
console.log(arr);               // ['a', 'b', 'c', 'd', 'e']

// fill - 填充数组
const numbers = [1, 2, 3, 4, 5];
numbers.fill(0);                // 用0填充整个数组
console.log(numbers);           // [0, 0, 0, 0, 0]

numbers.fill(1, 1, 4);         // 从索引1到4填充1
console.log(numbers);           // [0, 1, 1, 1, 0]

// copyWithin - 复制数组的一部分到其他位置
const array = [1, 2, 3, 4, 5];
array.copyWithin(0, 3);         // 将从位置3开始的元素复制到位置0
console.log(array);             // [4, 5, 3, 4, 5]
```

## 不修改数组的方法

### 1. 数组连接和切片

```javascript
const arr1 = [1, 2];
const arr2 = [3, 4];

// concat - 连接数组
const combined = arr1.concat(arr2);
console.log(combined);          // [1, 2, 3, 4]
console.log(arr1);             // [1, 2] (原数组未改变)

// slice - 切片
const numbers = [1, 2, 3, 4, 5];
const slice1 = numbers.slice(1, 3);
console.log(slice1);            // [2, 3]
console.log(numbers);           // [1, 2, 3, 4, 5] (原数组未改变)
```

### 2. 数组搜索方法

```javascript
const numbers = [1, 2, 3, 4, 5, 2];

// indexOf - 查找元素位置
console.log(numbers.indexOf(2));        // 1
console.log(numbers.indexOf(2, 2));     // 5 (从索引2开始搜索)

// lastIndexOf - 从后向前查找
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

## 迭代方法

### 1. 遍历方法

```javascript
const numbers = [1, 2, 3, 4, 5];

// forEach - 遍历数组
numbers.forEach((num, index) => {
    console.log(`Index ${index}: ${num}`);
});

// map - 映射数组
const doubled = numbers.map(num => num * 2);
console.log(doubled);           // [2, 4, 6, 8, 10]

// filter - 过滤数组
const evens = numbers.filter(num => num % 2 === 0);
console.log(evens);            // [2, 4]

// reduce - 归约数组
const sum = numbers.reduce((acc, cur) => acc + cur, 0);
console.log(sum);              // 15

// reduceRight - 从右向左归约
const result = numbers.reduceRight((acc, cur) => acc + cur, 0);
console.log(result);           // 15
```

### 2. 测试方法

```javascript
const numbers = [1, 2, 3, 4, 5];

// every - 检查所有元素是否满足条件
const allPositive = numbers.every(num => num > 0);
console.log(allPositive);      // true

// some - 检查是否存在满足条件的元素
const hasEven = numbers.some(num => num % 2 === 0);
console.log(hasEven);          // true

// entries - 返回键值对迭代器
for (const [index, value] of numbers.entries()) {
    console.log(`Index ${index}: ${value}`);
}

// keys - 返回索引迭代器
for (const index of numbers.keys()) {
    console.log(index);
}

// values - 返回值迭代器
for (const value of numbers.values()) {
    console.log(value);
}
```

## 数组转换方法

### 1. 字符串转换

```javascript
const arr = [1, 2, 3, 4, 5];

// toString - 转换为字符串
console.log(arr.toString());    // "1,2,3,4,5"

// join - 使用指定分隔符连接
console.log(arr.join());        // "1,2,3,4,5"
console.log(arr.join('-'));     // "1-2-3-4-5"
console.log(arr.join(''));      // "12345"

// 本地化字符串
console.log(arr.toLocaleString('zh-CN'));
```

### 2. 数组扁平化

```javascript
const nested = [1, [2, 3], [4, [5, 6]]];

// flat - 扁平化数组
console.log(nested.flat());     // [1, 2, 3, 4, [5, 6]]
console.log(nested.flat(2));    // [1, 2, 3, 4, 5, 6]

// flatMap - 映射并扁平化
const sentences = ['Hello World', 'Good Morning'];
const words = sentences.flatMap(s => s.split(' '));
console.log(words);            // ['Hello', 'World', 'Good', 'Morning']
```

## 实践应用

### 1. 数组操作工具

```javascript
class ArrayUtils {
    // 去重
    static unique(arr) {
        return Array.from(new Set(arr));
    }
    
    // 交集
    static intersection(arr1, arr2) {
        const set2 = new Set(arr2);
        return arr1.filter(item => set2.has(item));
    }
    
    // 差集
    static difference(arr1, arr2) {
        const set2 = new Set(arr2);
        return arr1.filter(item => !set2.has(item));
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
}
```

### 2. 数组排序工具

```javascript
class ArraySorter {
    // 自然排序
    static naturalSort(arr) {
        return arr.sort((a, b) => {
            return String(a).localeCompare(String(b), undefined, {
                numeric: true,
                sensitivity: 'base'
            });
        });
    }
    
    // 多重排序
    static multiSort(arr, ...criteria) {
        return arr.sort((a, b) => {
            for (const criterion of criteria) {
                const { key, direction = 'asc' } = criterion;
                const valueA = typeof key === 'function' ? key(a) : a[key];
                const valueB = typeof key === 'function' ? key(b) : b[key];
                
                if (valueA !== valueB) {
                    return direction === 'asc' 
                        ? valueA > valueB ? 1 : -1
                        : valueA < valueB ? 1 : -1;
                }
            }
            return 0;
        });
    }
}
```

### 3. 数组转换工具

```javascript
class ArrayTransformer {
    // 树形结构转换
    static toTree(arr, { idKey = 'id', parentKey = 'parentId', childrenKey = 'children' } = {}) {
        const map = new Map();
        const roots = [];
        
        // 创建节点映射
        arr.forEach(item => {
            map.set(item[idKey], { ...item, [childrenKey]: [] });
        });
        
        // 构建树结构
        arr.forEach(item => {
            const node = map.get(item[idKey]);
            if (item[parentKey] && map.has(item[parentKey])) {
                map.get(item[parentKey])[childrenKey].push(node);
            } else {
                roots.push(node);
            }
        });
        
        return roots;
    }
    
    // 分页
    static paginate(arr, page, pageSize) {
        const start = (page - 1) * pageSize;
        return arr.slice(start, start + pageSize);
    }
}
```

## 最佳实践

1. 方法选择
   ```javascript
   // 推荐：使用恰当的数组方法
   // 遍历用forEach
   array.forEach(item => console.log(item));
   
   // 转换用map
   const transformed = array.map(item => transform(item));
   
   // 过滤用filter
   const filtered = array.filter(item => condition(item));
   
   // 查找用find
   const found = array.find(item => condition(item));
   ```

2. 性能优化
   ```javascript
   // 推荐：避免频繁修改数组长度
   const arr = new Array(1000);
   
   // 推荐：使用适当的迭代方法
   // 提前终止迭代用some/every
   const hasNegative = numbers.some(n => n < 0);
   
   // 累积计算用reduce
   const sum = numbers.reduce((acc, cur) => acc + cur, 0);
   ```

3. 函数式编程
   ```javascript
   // 推荐：链式调用
   const result = array
       .filter(x => x > 0)
       .map(x => x * 2)
       .reduce((acc, cur) => acc + cur, 0);
   ```

## 总结

- 掌握修改数组的方法
- 理解不修改数组的方法
- 熟练使用迭代方法
- 掌握数组转换方法
- 实现实用工具类
- 遵循最佳实践

下一章将介绍JavaScript数组搜索。
