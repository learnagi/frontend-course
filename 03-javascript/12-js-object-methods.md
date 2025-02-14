---
title: "JavaScript对象方法"
slug: "javascript-object-methods"
sequence: 12
description: "详细介绍JavaScript对象方法的定义和使用"
is_published: true
estimated_minutes: 25
language: "zh-CN"
---

# JavaScript对象方法

## 方法定义

### 1. 基本方法定义

```javascript
// 对象字面量方法定义
const person = {
    name: '张三',
    sayHello() {
        console.log(`你好，我是${this.name}`);
    },
    // 传统方法定义（等效）
    greet: function() {
        console.log(`大家好，我是${this.name}`);
    }
};

// 后期添加方法
person.introduce = function() {
    console.log(`我叫${this.name}`);
};
```

### 2. 箭头函数方法

```javascript
const calculator = {
    numbers: [],
    // 普通方法
    addNumber(num) {
        this.numbers.push(num);
    },
    // 箭头函数方法（保持this上下文）
    calculateSum: () => {
        // 注意：箭头函数中this指向定义时的上下文
        return this.numbers.reduce((sum, num) => sum + num, 0);
    }
};
```

## this关键字

### 1. this绑定规则

```javascript
// 默认绑定
function showThis() {
    console.log(this);
}
showThis(); // window或undefined（严格模式）

// 隐式绑定
const user = {
    name: '李四',
    sayName() {
        console.log(this.name);
    }
};
user.sayName(); // "李四"

// 显式绑定
function greet() {
    console.log(`你好，${this.name}`);
}
const person1 = { name: '王五' };
greet.call(person1);   // "你好，王五"
greet.apply(person1);  // "你好，王五"
const boundGreet = greet.bind(person1);
boundGreet();         // "你好，王五"
```

### 2. this问题解决方案

```javascript
const app = {
    name: 'MyApp',
    users: ['张三', '李四', '王五'],
    
    // 方法一：使用箭头函数
    printUsers1() {
        this.users.forEach((user) => {
            console.log(`${this.name}: ${user}`);
        });
    },
    
    // 方法二：保存this引用
    printUsers2() {
        const self = this;
        this.users.forEach(function(user) {
            console.log(`${self.name}: ${user}`);
        });
    },
    
    // 方法三：使用bind
    printUsers3() {
        this.users.forEach(function(user) {
            console.log(`${this.name}: ${user}`);
        }.bind(this));
    }
};
```

## 方法继承

### 1. 原型方法

```javascript
// 构造函数
function Animal(name) {
    this.name = name;
}

// 原型方法
Animal.prototype.makeSound = function() {
    console.log('Some sound');
};

// 继承
function Dog(name) {
    Animal.call(this, name);
}

Dog.prototype = Object.create(Animal.prototype);
Dog.prototype.constructor = Dog;

// 重写方法
Dog.prototype.makeSound = function() {
    console.log('Woof!');
};

const dog = new Dog('旺财');
dog.makeSound(); // "Woof!"
```

### 2. 类方法

```javascript
class Animal {
    constructor(name) {
        this.name = name;
    }
    
    // 实例方法
    makeSound() {
        console.log('Some sound');
    }
    
    // 静态方法
    static create(name) {
        return new this(name);
    }
}

class Dog extends Animal {
    makeSound() {
        super.makeSound(); // 调用父类方法
        console.log('Woof!');
    }
}
```

## 方法类型

### 1. 实例方法

```javascript
class User {
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }
    
    // 实例方法
    introduce() {
        return `我叫${this.name}，今年${this.age}岁`;
    }
    
    celebrate() {
        this.age++;
        return `今天是我的生日，现在${this.age}岁了！`;
    }
}

const user = new User('张三', 25);
console.log(user.introduce());
```

### 2. 静态方法

```javascript
class MathHelper {
    // 静态方法
    static add(x, y) {
        return x + y;
    }
    
    static multiply(x, y) {
        return x * y;
    }
    
    static square(x) {
        return x * x;
    }
    
    // 工厂方法
    static createPoint(x, y) {
        return { x, y };
    }
}

console.log(MathHelper.add(5, 3));      // 8
console.log(MathHelper.square(4));      // 16
```

### 3. 访问器方法

```javascript
class Circle {
    constructor(radius) {
        this._radius = radius;
    }
    
    // getter方法
    get radius() {
        return this._radius;
    }
    
    // setter方法
    set radius(value) {
        if (value <= 0) {
            throw new Error('半径必须大于0');
        }
        this._radius = value;
    }
    
    // 计算属性方法
    get area() {
        return Math.PI * this._radius ** 2;
    }
    
    get circumference() {
        return 2 * Math.PI * this._radius;
    }
}
```

## 方法装饰器

### 1. 日志装饰器

```javascript
function log(target, name, descriptor) {
    const original = descriptor.value;
    
    descriptor.value = function(...args) {
        console.log(`调用方法 ${name} 参数:`, args);
        const result = original.apply(this, args);
        console.log(`方法 ${name} 返回:`, result);
        return result;
    };
    
    return descriptor;
}

class Calculator {
    @log
    add(a, b) {
        return a + b;
    }
}
```

### 2. 性能监控装饰器

```javascript
function measure(target, name, descriptor) {
    const original = descriptor.value;
    
    descriptor.value = function(...args) {
        const start = performance.now();
        const result = original.apply(this, args);
        const end = performance.now();
        console.log(`${name} 执行时间: ${end - start}ms`);
        return result;
    };
    
    return descriptor;
}

class DataProcessor {
    @measure
    processData(data) {
        // 处理数据...
    }
}
```

## 实践示例

### 1. 方法链式调用

```javascript
class QueryBuilder {
    constructor() {
        this.query = {};
    }
    
    where(field, value) {
        this.query[field] = value;
        return this;
    }
    
    limit(count) {
        this.query.limit = count;
        return this;
    }
    
    sort(field, order = 'asc') {
        this.query.sort = { field, order };
        return this;
    }
    
    build() {
        return this.query;
    }
}

// 使用示例
const query = new QueryBuilder()
    .where('age', 25)
    .limit(10)
    .sort('name', 'desc')
    .build();
```

### 2. 方法组合

```javascript
class StringProcessor {
    constructor(str) {
        this.str = str;
    }
    
    trim() {
        this.str = this.str.trim();
        return this;
    }
    
    capitalize() {
        this.str = this.str.charAt(0).toUpperCase() + 
                   this.str.slice(1);
        return this;
    }
    
    reverse() {
        this.str = this.str.split('').reverse().join('');
        return this;
    }
    
    get value() {
        return this.str;
    }
}

// 使用示例
const processor = new StringProcessor('  hello world  ');
const result = processor
    .trim()
    .capitalize()
    .value;  // "Hello world"
```

## 最佳实践

1. 方法命名
   ```javascript
   class User {
       // 动词开头，表示动作
       getName() { }
       setAge() { }
       
       // is/has开头，返回布尔值
       isActive() { }
       hasPermission() { }
       
       // get开头，获取计算值
       getFullName() { }
   }
   ```

2. 单一职责
   ```javascript
   // 好的实践
   class OrderProcessor {
       validateOrder() { }
       calculateTotal() { }
       processPayment() { }
   }
   
   // 避免
   class Order {
       doEverything() { }
   }
   ```

3. 错误处理
   ```javascript
   class BankAccount {
       withdraw(amount) {
           if (amount <= 0) {
               throw new Error('提款金额必须大于0');
           }
           if (amount > this.balance) {
               throw new Error('余额不足');
           }
           this.balance -= amount;
           return this.balance;
       }
   }
   ```

## 总结

- 掌握方法定义方式
- 理解this关键字
- 使用方法继承
- 区分方法类型
- 应用方法装饰器
- 遵循最佳实践

下一章将介绍JavaScript对象显示。
