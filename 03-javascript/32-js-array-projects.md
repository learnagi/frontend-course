---
title: "JavaScript数组项目实战"
slug: "javascript-array-projects"
sequence: 32
description: "通过实际项目案例学习JavaScript数组的应用"
---

# JavaScript数组项目实战

本章将通过几个实际的项目案例，展示JavaScript数组在实际开发中的应用。

## 项目一：数据分析工具

### 1. 数据处理类

```javascript
class DataAnalyzer {
    constructor(data) {
        this.data = data;
        this.dimensions = Object.keys(data[0] || {});
    }
    
    // 数据分组
    groupBy(dimension) {
        return this.data.reduce((groups, item) => {
            const key = item[dimension];
            if (!groups[key]) {
                groups[key] = [];
            }
            groups[key].push(item);
            return groups;
        }, {});
    }
    
    // 聚合计算
    aggregate(dimension, metric, aggregator) {
        const groups = this.groupBy(dimension);
        
        return Object.entries(groups).map(([key, group]) => ({
            [dimension]: key,
            [metric]: this.calculateAggregation(group, metric, aggregator)
        }));
    }
    
    // 计算聚合值
    calculateAggregation(group, metric, aggregator) {
        const values = group.map(item => item[metric]);
        
        switch (aggregator) {
            case 'sum':
                return values.reduce((a, b) => a + b, 0);
            case 'avg':
                return values.reduce((a, b) => a + b, 0) / values.length;
            case 'max':
                return Math.max(...values);
            case 'min':
                return Math.min(...values);
            default:
                return values.length;
        }
    }
    
    // 数据过滤
    filter(conditions) {
        return new DataAnalyzer(
            this.data.filter(item =>
                Object.entries(conditions).every(([key, value]) =>
                    item[key] === value
                )
            )
        );
    }
    
    // 数据排序
    sort(dimension, direction = 'asc') {
        return new DataAnalyzer(
            [...this.data].sort((a, b) => {
                const valueA = a[dimension];
                const valueB = b[dimension];
                return direction === 'asc'
                    ? valueA < valueB ? -1 : valueA > valueB ? 1 : 0
                    : valueB < valueA ? -1 : valueB > valueA ? 1 : 0;
            })
        );
    }
}

// 使用示例
const salesData = [
    { date: '2023-01', product: 'A', sales: 100, region: 'North' },
    { date: '2023-01', product: 'B', sales: 200, region: 'North' },
    { date: '2023-02', product: 'A', sales: 150, region: 'South' },
    { date: '2023-02', product: 'B', sales: 180, region: 'South' }
];

const analyzer = new DataAnalyzer(salesData);

// 按产品分组并计算销售总额
const productSales = analyzer.aggregate('product', 'sales', 'sum');
console.log('Product Sales:', productSales);

// 按地区筛选并排序
const northRegion = analyzer
    .filter({ region: 'North' })
    .sort('sales', 'desc');
console.log('North Region Sales:', northRegion.data);
```

## 项目二：任务管理系统

### 1. 任务管理器

```javascript
class Task {
    constructor(id, title, description, dueDate, priority, status = 'pending') {
        this.id = id;
        this.title = title;
        this.description = description;
        this.dueDate = new Date(dueDate);
        this.priority = priority;
        this.status = status;
        this.createdAt = new Date();
        this.updatedAt = new Date();
    }
}

class TaskManager {
    constructor() {
        this.tasks = [];
    }
    
    // 添加任务
    addTask(taskData) {
        const task = new Task(
            Date.now(),
            taskData.title,
            taskData.description,
            taskData.dueDate,
            taskData.priority
        );
        this.tasks.push(task);
        return task;
    }
    
    // 更新任务
    updateTask(id, updates) {
        const index = this.tasks.findIndex(task => task.id === id);
        if (index === -1) return null;
        
        const task = this.tasks[index];
        Object.assign(task, updates, {
            updatedAt: new Date()
        });
        
        return task;
    }
    
    // 删除任务
    deleteTask(id) {
        const index = this.tasks.findIndex(task => task.id === id);
        if (index === -1) return false;
        
        this.tasks.splice(index, 1);
        return true;
    }
    
    // 获取任务列表
    getTasks(filters = {}) {
        return this.tasks.filter(task =>
            Object.entries(filters).every(([key, value]) =>
                task[key] === value
            )
        );
    }
    
    // 获取待办任务
    getPendingTasks() {
        return this.getTasks({ status: 'pending' })
            .sort((a, b) => a.dueDate - b.dueDate);
    }
    
    // 获取已完成任务
    getCompletedTasks() {
        return this.getTasks({ status: 'completed' })
            .sort((a, b) => b.updatedAt - a.updatedAt);
    }
    
    // 获取逾期任务
    getOverdueTasks() {
        const now = new Date();
        return this.getTasks({ status: 'pending' })
            .filter(task => task.dueDate < now)
            .sort((a, b) => a.dueDate - b.dueDate);
    }
    
    // 任务统计
    getStatistics() {
        return {
            total: this.tasks.length,
            pending: this.getPendingTasks().length,
            completed: this.getCompletedTasks().length,
            overdue: this.getOverdueTasks().length
        };
    }
}

// 使用示例
const taskManager = new TaskManager();

// 添加任务
taskManager.addTask({
    title: '完成项目文档',
    description: '编写项目技术文档和使用说明',
    dueDate: '2024-03-01',
    priority: 'high'
});

// 添加更多任务
taskManager.addTask({
    title: '代码审查',
    description: '审查团队提交的代码',
    dueDate: '2024-02-28',
    priority: 'medium'
});

// 更新任务状态
const tasks = taskManager.getTasks();
if (tasks.length > 0) {
    taskManager.updateTask(tasks[0].id, {
        status: 'completed'
    });
}

// 获取统计信息
console.log('Task Statistics:', taskManager.getStatistics());
```

## 项目三：购物车系统

### 1. 购物车管理器

```javascript
class Product {
    constructor(id, name, price, stock) {
        this.id = id;
        this.name = name;
        this.price = price;
        this.stock = stock;
    }
}

class CartItem {
    constructor(product, quantity) {
        this.product = product;
        this.quantity = quantity;
    }
    
    get total() {
        return this.product.price * this.quantity;
    }
}

class ShoppingCart {
    constructor() {
        this.items = [];
    }
    
    // 添加商品
    addItem(product, quantity = 1) {
        if (product.stock < quantity) {
            throw new Error('库存不足');
        }
        
        const existingItem = this.items.find(
            item => item.product.id === product.id
        );
        
        if (existingItem) {
            if (product.stock < existingItem.quantity + quantity) {
                throw new Error('库存不足');
            }
            existingItem.quantity += quantity;
        } else {
            this.items.push(new CartItem(product, quantity));
        }
        
        return this.items;
    }
    
    // 更新商品数量
    updateQuantity(productId, quantity) {
        const item = this.items.find(
            item => item.product.id === productId
        );
        
        if (!item) {
            throw new Error('商品不存在');
        }
        
        if (item.product.stock < quantity) {
            throw new Error('库存不足');
        }
        
        item.quantity = quantity;
        return item;
    }
    
    // 移除商品
    removeItem(productId) {
        const index = this.items.findIndex(
            item => item.product.id === productId
        );
        
        if (index !== -1) {
            this.items.splice(index, 1);
        }
    }
    
    // 清空购物车
    clear() {
        this.items = [];
    }
    
    // 获取总价
    get total() {
        return this.items.reduce(
            (sum, item) => sum + item.total,
            0
        );
    }
    
    // 获取商品总数
    get itemCount() {
        return this.items.reduce(
            (count, item) => count + item.quantity,
            0
        );
    }
    
    // 获取购物车摘要
    getSummary() {
        return {
            items: this.items.map(item => ({
                productId: item.product.id,
                name: item.product.name,
                price: item.product.price,
                quantity: item.quantity,
                total: item.total
            })),
            totalItems: this.itemCount,
            totalAmount: this.total
        };
    }
}

// 使用示例
const products = [
    new Product(1, 'iPhone 15', 999, 10),
    new Product(2, 'AirPods Pro', 249, 20),
    new Product(3, 'MacBook Pro', 1999, 5)
];

const cart = new ShoppingCart();

// 添加商品
cart.addItem(products[0], 2);
cart.addItem(products[1], 1);

// 更新数量
cart.updateQuantity(1, 3);

// 获取购物车摘要
console.log('Cart Summary:', cart.getSummary());
```

## 最佳实践

1. 数据结构设计
   ```javascript
   // 使用类封装数据和行为
   class DataStructure {
       constructor(data) {
           this.data = data;
           this.index = new Map();
           this.buildIndex();
       }
       
       buildIndex() {
           this.data.forEach((item, index) => {
               this.index.set(item.id, index);
           });
       }
       
       find(id) {
           const index = this.index.get(id);
           return index !== undefined ? this.data[index] : null;
       }
   }
   ```

2. 错误处理
   ```javascript
   // 使用自定义错误类
   class BusinessError extends Error {
       constructor(code, message) {
           super(message);
           this.code = code;
       }
   }
   
   // 统一错误处理
   const handleOperation = (operation) => {
       try {
           return operation();
       } catch (error) {
           if (error instanceof BusinessError) {
               console.error(`业务错误 [${error.code}]:`, error.message);
           } else {
               console.error('系统错误:', error);
           }
           throw error;
       }
   };
   ```

3. 性能优化
   ```javascript
   // 使用缓存优化性能
   class CachedManager {
       constructor() {
           this.cache = new Map();
           this.data = [];
       }
       
       getItem(id) {
           if (this.cache.has(id)) {
               return this.cache.get(id);
           }
           
           const item = this.data.find(item => item.id === id);
           if (item) {
               this.cache.set(id, item);
           }
           return item;
       }
       
       invalidateCache() {
           this.cache.clear();
       }
   }
   ```

## 总结

- 实现数据分析工具
- 开发任务管理系统
- 构建购物车功能
- 掌握项目最佳实践
- 注意性能优化
- 处理异常情况

下一章将总结JavaScript数组的学习要点。
