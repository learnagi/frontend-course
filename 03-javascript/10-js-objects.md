---
title: "JavaScript对象"
slug: "javascript-objects"
sequence: 10
description: "详细介绍JavaScript对象的基本概念和使用方法"
is_published: true
estimated_minutes: 25
language: "zh-CN"
---

# JavaScript对象

## 对象基础

### 1. 对象创建

```javascript
// 对象字面量
const person = {
    name: "张三",
    age: 25
};

// 使用new Object()
const car = new Object();
car.brand = "Toyota";
car.model = "Camry";

// 工厂函数
function createPerson(name, age) {
    return {
        name: name,
        age: age
    };
}
```

### 2. 对象属性

```javascript
// 点号访问
const user = {
    name: "李四",
    age: 30
};
console.log(user.name);  // "李四"

// 方括号访问
const propertyName = "age";
console.log(user[propertyName]);  // 30

// 属性简写
const x = 10, y = 20;
const point = { x, y };  // 等同于 { x: x, y: y }
```

## 对象特性

### 1. 属性特性

```javascript
// 属性描述符
const person = {};
Object.defineProperty(person, 'name', {
    value: '张三',
    writable: true,     // 是否可写
    enumerable: true,   // 是否可枚举
    configurable: true  // 是否可配置
});

// 获取属性描述符
console.log(Object.getOwnPropertyDescriptor(person, 'name'));

// 定义多个属性
Object.defineProperties(person, {
    age: {
        value: 25,
        writable: true
    },
    gender: {
        value: '男',
        writable: false
    }
});
```

### 2. 对象状态

```javascript
// 对象冻结
const settings = {
    apiUrl: 'https://api.example.com',
    timeout: 5000
};
Object.freeze(settings);
// settings.timeout = 6000;  // 错误：无法修改

// 对象密封
const config = {
    theme: 'dark',
    language: 'zh-CN'
};
Object.seal(config);
config.language = 'en';  // 可以修改现有属性
// config.newProp = 'value';  // 错误：无法添加新属性

// 对象防扩展
const data = {
    count: 0
};
Object.preventExtensions(data);
data.count++;  // 可以修改现有属性
// data.newProp = 'value';  // 错误：无法添加新属性
```

## 对象操作

### 1. 遍历对象

```javascript
const user = {
    name: '王五',
    age: 35,
    city: '北京'
};

// for...in 循环
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

### 2. 对象合并

```javascript
// Object.assign()
const target = { a: 1, b: 2 };
const source = { b: 4, c: 5 };
const result = Object.assign(target, source);
// result: { a: 1, b: 4, c: 5 }

// 展开运算符
const obj1 = { foo: 'bar', x: 42 };
const obj2 = { foo: 'baz', y: 13 };
const clonedObj = { ...obj1 };
const mergedObj = { ...obj1, ...obj2 };
```

## 对象原型

### 1. 原型链

```javascript
// 原型继承
const animal = {
    makeSound() {
        console.log('Some sound');
    }
};

const dog = Object.create(animal);
dog.bark = function() {
    console.log('Woof!');
};

// 检查原型
console.log(Object.getPrototypeOf(dog) === animal);  // true
console.log(dog.isPrototypeOf(animal));             // false
console.log(animal.isPrototypeOf(dog));             // true
```

### 2. 原型方法

```javascript
// hasOwnProperty
const person = {
    name: '赵六',
    age: 40
};

console.log(person.hasOwnProperty('name'));     // true
console.log(person.hasOwnProperty('toString')); // false

// instanceof
function Car(make, model) {
    this.make = make;
    this.model = model;
}

const myCar = new Car('Honda', 'Civic');
console.log(myCar instanceof Car);    // true
console.log(myCar instanceof Object); // true
```

## 高级特性

### 1. getter和setter

```javascript
const person = {
    firstName: '张',
    lastName: '三',
    get fullName() {
        return `${this.firstName}${this.lastName}`;
    },
    set fullName(name) {
        [this.firstName, this.lastName] = name.split('');
    }
};

console.log(person.fullName);  // "张三"
person.fullName = '李四';
console.log(person.firstName); // "李"
console.log(person.lastName);  // "四"
```

### 2. 代理对象

```javascript
// 基本代理
const target = {
    name: '张三',
    age: 25
};

const handler = {
    get(target, prop) {
        console.log(`访问属性：${prop}`);
        return target[prop];
    },
    set(target, prop, value) {
        console.log(`设置属性：${prop} = ${value}`);
        target[prop] = value;
        return true;
    }
};

const proxy = new Proxy(target, handler);

// 验证代理
const validator = {
    set(target, prop, value) {
        if (prop === 'age') {
            if (!Number.isInteger(value)) {
                throw new TypeError('年龄必须是整数');
            }
            if (value < 0 || value > 150) {
                throw new RangeError('年龄必须在0-150之间');
            }
        }
        target[prop] = value;
        return true;
    }
};

const person = new Proxy({}, validator);
```

## 实践示例

### 1. 深度克隆

```javascript
function deepClone(obj) {
    // 处理基本类型和null
    if (obj === null || typeof obj !== 'object') {
        return obj;
    }
    
    // 处理日期对象
    if (obj instanceof Date) {
        return new Date(obj.getTime());
    }
    
    // 处理数组
    if (Array.isArray(obj)) {
        return obj.map(item => deepClone(item));
    }
    
    // 处理对象
    const clonedObj = {};
    Object.keys(obj).forEach(key => {
        clonedObj[key] = deepClone(obj[key]);
    });
    
    return clonedObj;
}
```

### 2. 对象观察者

```javascript
class Observable {
    constructor() {
        this.observers = new Set();
    }
    
    subscribe(observer) {
        this.observers.add(observer);
    }
    
    unsubscribe(observer) {
        this.observers.delete(observer);
    }
    
    notify(data) {
        this.observers.forEach(observer => observer(data));
    }
}

// 使用示例
const userStore = new Observable();
userStore.subscribe(user => console.log('用户更新：', user));
```

## 最佳实践

1. 属性命名
   ```javascript
   // 使用有意义的属性名
   const good = {
       firstName: 'John',
       lastName: 'Doe',
       dateOfBirth: '1990-01-01'
   };

   // 避免使用
   const bad = {
       fn: 'John',
       ln: 'Doe',
       dob: '1990-01-01'
   };
   ```

2. 数据访问
   ```javascript
   // 使用解构
   const { name, age } = person;

   // 使用默认值
   const { theme = 'light' } = settings;

   // 重命名
   const { name: userName } = user;
   ```

3. 对象组织
   ```javascript
   // 相关属性分组
   const user = {
       // 个人信息
       profile: {
           name: '张三',
           age: 25,
           gender: '男'
       },
       // 联系方式
       contact: {
           email: 'zhangsan@example.com',
           phone: '123456789'
       }
   };
   ```

## 总结

- 理解对象基础概念
- 掌握对象属性操作
- 了解对象特性和状态
- 使用原型和继承
- 实现高级特性
- 遵循最佳实践

下一章将介绍JavaScript对象属性。
