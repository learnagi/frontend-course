---
title: "JavaScript数组实战应用"
slug: "javascript-array-applications"
sequence: 30
description: "通过实际案例深入学习JavaScript数组的应用"
---

# JavaScript数组实战应用

本章将通过实际案例，展示JavaScript数组在实际开发中的应用场景和最佳实践。

## 数据处理应用

### 1. 数据转换和格式化

```javascript
// 处理CSV数据
const parseCSV = (csvString) => {
    return csvString
        .split('\n')
        .map(row => row.split(','))
        .map(([id, name, age]) => ({
            id: parseInt(id),
            name: name.trim(),
            age: parseInt(age)
        }));
};

// 使用示例
const csvData = `
1,John Doe,25
2,Jane Smith,30
3,Bob Johnson,35
`;

const users = parseCSV(csvData.trim());
console.log(users);
```

### 2. 数据统计分析

```javascript
// 数据统计工具
const statistics = {
    average: arr => arr.reduce((sum, val) => sum + val, 0) / arr.length,
    
    median: arr => {
        const sorted = [...arr].sort((a, b) => a - b);
        const mid = Math.floor(sorted.length / 2);
        return sorted.length % 2 === 0
            ? (sorted[mid - 1] + sorted[mid]) / 2
            : sorted[mid];
    },
    
    mode: arr => {
        const frequency = arr.reduce((freq, val) => {
            freq[val] = (freq[val] || 0) + 1;
            return freq;
        }, {});
        
        return Object.entries(frequency)
            .reduce((mode, [val, count]) => 
                count > mode.count ? { value: val, count } : mode,
                { value: null, count: 0 }
            ).value;
    }
};

// 使用示例
const data = [1, 2, 2, 3, 4, 4, 4, 5];
console.log('Average:', statistics.average(data));
console.log('Median:', statistics.median(data));
console.log('Mode:', statistics.mode(data));
```

## 用户界面应用

### 1. 表格数据管理

```javascript
class DataTable {
    constructor(data) {
        this.data = data;
        this.sortField = null;
        this.sortDirection = 'asc';
        this.filters = {};
    }
    
    sort(field) {
        if (field === this.sortField) {
            this.sortDirection = this.sortDirection === 'asc' ? 'desc' : 'asc';
        } else {
            this.sortField = field;
            this.sortDirection = 'asc';
        }
        
        return this.getDisplayData();
    }
    
    filter(field, value) {
        if (value) {
            this.filters[field] = value;
        } else {
            delete this.filters[field];
        }
        
        return this.getDisplayData();
    }
    
    getDisplayData() {
        let result = [...this.data];
        
        // 应用过滤
        Object.entries(this.filters).forEach(([field, value]) => {
            result = result.filter(item => 
                String(item[field]).toLowerCase()
                    .includes(String(value).toLowerCase())
            );
        });
        
        // 应用排序
        if (this.sortField) {
            result.sort((a, b) => {
                const valueA = a[this.sortField];
                const valueB = b[this.sortField];
                
                if (this.sortDirection === 'asc') {
                    return valueA < valueB ? -1 : valueA > valueB ? 1 : 0;
                } else {
                    return valueA > valueB ? -1 : valueA < valueB ? 1 : 0;
                }
            });
        }
        
        return result;
    }
}

// 使用示例
const tableData = [
    { id: 1, name: 'Product A', price: 99.99 },
    { id: 2, name: 'Product B', price: 149.99 },
    { id: 3, name: 'Product C', price: 79.99 }
];

const table = new DataTable(tableData);
console.log(table.sort('price'));
console.log(table.filter('name', 'Product'));
```

### 2. 虚拟列表实现

```javascript
class VirtualList {
    constructor(items, rowHeight, visibleRows) {
        this.items = items;
        this.rowHeight = rowHeight;
        this.visibleRows = visibleRows;
        this.scrollTop = 0;
    }
    
    getVisibleItems() {
        const startIndex = Math.floor(this.scrollTop / this.rowHeight);
        const endIndex = Math.min(
            startIndex + this.visibleRows,
            this.items.length
        );
        
        return {
            items: this.items.slice(startIndex, endIndex),
            startIndex,
            totalHeight: this.items.length * this.rowHeight,
            offsetY: startIndex * this.rowHeight
        };
    }
    
    scrollTo(scrollTop) {
        this.scrollTop = Math.max(0, Math.min(
            scrollTop,
            (this.items.length - this.visibleRows) * this.rowHeight
        ));
        return this.getVisibleItems();
    }
}
```

## 游戏开发应用

### 1. 网格系统

```javascript
class Grid {
    constructor(width, height) {
        this.width = width;
        this.height = height;
        this.cells = Array.from({ length: height }, () =>
            Array(width).fill(null)
        );
    }
    
    set(x, y, value) {
        if (this.isValidPosition(x, y)) {
            this.cells[y][x] = value;
            return true;
        }
        return false;
    }
    
    get(x, y) {
        return this.isValidPosition(x, y) ? this.cells[y][x] : null;
    }
    
    isValidPosition(x, y) {
        return x >= 0 && x < this.width && y >= 0 && y < this.height;
    }
    
    getNeighbors(x, y) {
        const directions = [
            [-1, -1], [0, -1], [1, -1],
            [-1, 0],           [1, 0],
            [-1, 1],  [0, 1],  [1, 1]
        ];
        
        return directions
            .map(([dx, dy]) => [x + dx, y + dy])
            .filter(([nx, ny]) => this.isValidPosition(nx, ny))
            .map(([nx, ny]) => this.get(nx, ny));
    }
}
```

### 2. 粒子系统

```javascript
class ParticleSystem {
    constructor() {
        this.particles = [];
    }
    
    createParticle(x, y, velocity, lifetime) {
        return {
            x, y,
            vx: velocity.x,
            vy: velocity.y,
            lifetime,
            age: 0
        };
    }
    
    emit(count, config) {
        for (let i = 0; i < count; i++) {
            const angle = Math.random() * Math.PI * 2;
            const speed = config.minSpeed + 
                Math.random() * (config.maxSpeed - config.minSpeed);
            
            this.particles.push(
                this.createParticle(
                    config.x,
                    config.y,
                    {
                        x: Math.cos(angle) * speed,
                        y: Math.sin(angle) * speed
                    },
                    config.lifetime
                )
            );
        }
    }
    
    update(deltaTime) {
        this.particles = this.particles
            .filter(p => p.age < p.lifetime)
            .map(p => ({
                ...p,
                x: p.x + p.vx * deltaTime,
                y: p.y + p.vy * deltaTime,
                age: p.age + deltaTime
            }));
    }
}
```

## 数据可视化应用

### 1. 图表数据处理

```javascript
class ChartDataProcessor {
    constructor(data) {
        this.data = data;
    }
    
    groupBy(key, aggregator = 'count') {
        const groups = this.data.reduce((acc, item) => {
            const groupKey = item[key];
            if (!acc[groupKey]) {
                acc[groupKey] = [];
            }
            acc[groupKey].push(item);
            return acc;
        }, {});
        
        return Object.entries(groups).map(([key, values]) => ({
            key,
            value: this.aggregate(values, aggregator)
        }));
    }
    
    aggregate(values, aggregator) {
        switch (aggregator) {
            case 'count':
                return values.length;
            case 'sum':
                return values.reduce((sum, v) => sum + v.value, 0);
            case 'average':
                return values.reduce((sum, v) => sum + v.value, 0) / values.length;
            default:
                return values;
        }
    }
    
    getTimeSeriesData(dateField, valueField, interval = 'day') {
        const sorted = [...this.data].sort((a, b) => 
            new Date(a[dateField]) - new Date(b[dateField])
        );
        
        return this.groupByTime(sorted, dateField, valueField, interval);
    }
    
    groupByTime(data, dateField, valueField, interval) {
        const groups = new Map();
        
        data.forEach(item => {
            const date = new Date(item[dateField]);
            const key = this.getTimeKey(date, interval);
            
            if (!groups.has(key)) {
                groups.set(key, []);
            }
            groups.get(key).push(item[valueField]);
        });
        
        return Array.from(groups.entries()).map(([key, values]) => ({
            date: key,
            value: values.reduce((sum, v) => sum + v, 0) / values.length
        }));
    }
    
    getTimeKey(date, interval) {
        switch (interval) {
            case 'hour':
                return new Date(
                    date.getFullYear(),
                    date.getMonth(),
                    date.getDate(),
                    date.getHours()
                );
            case 'day':
                return new Date(
                    date.getFullYear(),
                    date.getMonth(),
                    date.getDate()
                );
            case 'month':
                return new Date(
                    date.getFullYear(),
                    date.getMonth()
                );
            default:
                return date;
        }
    }
}
```

## 最佳实践

1. 数据处理
   ```javascript
   // 使用适当的数据结构
   const cache = new Map();  // 键值对缓存
   const uniqueItems = new Set();  // 唯一值集合
   
   // 链式处理
   const result = data
       .filter(validate)
       .map(transform)
       .reduce(aggregate);
   ```

2. 性能优化
   ```javascript
   // 批量处理
   const batchProcess = (items, batchSize = 1000) => {
       return new Promise(resolve => {
           const results = [];
           let index = 0;
           
           function processNextBatch() {
               const batch = items.slice(index, index + batchSize);
               if (batch.length === 0) {
                   resolve(results);
                   return;
               }
               
               results.push(...processBatch(batch));
               index += batchSize;
               setTimeout(processNextBatch, 0);
           }
           
           processNextBatch();
       });
   };
   ```

3. 错误处理
   ```javascript
   // 安全的数组操作
   const safeArrayOps = {
       get: (arr, index, defaultValue = null) => {
           return index >= 0 && index < arr.length
               ? arr[index]
               : defaultValue;
       },
       
       update: (arr, index, value) => {
           if (index >= 0 && index < arr.length) {
               const copy = [...arr];
               copy[index] = value;
               return copy;
           }
           return arr;
       }
   };
   ```

## 总结

- 掌握数据处理技巧
- 实现用户界面功能
- 开发游戏系统组件
- 处理数据可视化需求
- 注意性能优化
- 遵循最佳实践

下一章将介绍JavaScript数组的测试和调试技巧。
