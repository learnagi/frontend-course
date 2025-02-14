---
title: "JavaScript对象构造函数"
slug: "javascript-object-constructors"
sequence: 14
description: "详细介绍JavaScript对象构造函数的使用方法和最佳实践"
is_published: true
estimated_minutes: 25
language: "zh-CN"
---

# JavaScript对象构造函数

## 构造函数基础

### 1. 构造函数定义

```javascript
// 基本构造函数
function Person(name, age) {
    this.name = name;
    this.age = age;
    this.sayHello = function() {
        console.log(`你好，我是${this.name}`);
    };
}

// 使用构造函数
const person1 = new Person('张三', 25);
const person2 = new Person('李四', 30);

person1.sayHello(); // "你好，我是张三"
person2.sayHello(); // "你好，我是李四"
```

### 2. new操作符

```javascript
// new操作符的作用
function Car(make, model) {
    // 1. 创建新对象
    // 2. 设置原型
    // 3. 绑定this
    // 4. 返回新对象
    this.make = make;
    this.model = model;
}

// 模拟new操作符
function createObject(Constructor, ...args) {
    // 1. 创建新对象，并链接到原型
    const obj = Object.create(Constructor.prototype);
    
    // 2. 执行构造函数，绑定this
    const result = Constructor.apply(obj, args);
    
    // 3. 返回新对象或构造函数的返回值
    return (typeof result === 'object' && result !== null) 
        ? result 
        : obj;
}
```

## 原型和继承

### 1. 原型链

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
function Dog(name, breed) {
    // 调用父类构造函数
    Animal.call(this, name);
    this.breed = breed;
}

// 设置原型链
Dog.prototype = Object.create(Animal.prototype);
Dog.prototype.constructor = Dog;

// 添加子类方法
Dog.prototype.bark = function() {
    console.log('Woof!');
};

const dog = new Dog('旺财', '柴犬');
dog.makeSound(); // "Some sound"
dog.bark();      // "Woof!"
```

### 2. 构造函数继承

```javascript
// 基类
function Vehicle(type) {
    this.type = type;
}

Vehicle.prototype.getType = function() {
    return this.type;
};

// 派生类
function Car(make, model) {
    // 调用基类构造函数
    Vehicle.call(this, 'car');
    
    this.make = make;
    this.model = model;
}

// 原型继承
Car.prototype = Object.create(Vehicle.prototype);
Car.prototype.constructor = Car;

// 添加方法
Car.prototype.getInfo = function() {
    return `${this.make} ${this.model}`;
};
```

## 构造函数模式

### 1. 工厂构造函数

```javascript
// 工厂函数
function createPerson(name, age) {
    return {
        name: name,
        age: age,
        sayHello() {
            console.log(`你好，我是${this.name}`);
        }
    };
}

// 构造函数工厂
function PersonFactory() {
    return function(name, age) {
        return new Person(name, age);
    };
}

const createNewPerson = PersonFactory();
const person = createNewPerson('张三', 25);
```

### 2. 单例构造函数

```javascript
// 单例模式
const Singleton = (function() {
    let instance;
    
    function createInstance(config) {
        return {
            config: config,
            timestamp: Date.now()
        };
    }
    
    return {
        getInstance: function(config) {
            if (!instance) {
                instance = createInstance(config);
            }
            return instance;
        }
    };
})();

const instance1 = Singleton.getInstance({ theme: 'dark' });
const instance2 = Singleton.getInstance({ theme: 'light' });
console.log(instance1 === instance2); // true
```

## 高级构造函数

### 1. 参数验证

```javascript
function User(config) {
    // 参数验证
    if (!config.name) {
        throw new Error('用户名是必需的');
    }
    
    if (typeof config.age !== 'number') {
        throw new TypeError('年龄必须是数字');
    }
    
    // 属性初始化
    this.name = config.name;
    this.age = config.age;
    this.email = config.email || `${this.name}@example.com`;
}

// 使用示例
try {
    const user = new User({
        name: '张三',
        age: '25' // 错误：不是数字
    });
} catch (error) {
    console.error(error.message);
}
```

### 2. 私有属性

```javascript
// 使用Symbol实现私有属性
const _name = Symbol('name');
const _age = Symbol('age');

class Person {
    constructor(name, age) {
        this[_name] = name;
        this[_age] = age;
    }
    
    getName() {
        return this[_name];
    }
    
    getAge() {
        return this[_age];
    }
}

// 使用闭包实现私有属性
function createPerson(name, age) {
    // 私有变量
    let _name = name;
    let _age = age;
    
    // 返回对象
    return {
        getName() {
            return _name;
        },
        setName(name) {
            _name = name;
        }
    };
}
```

## 构造函数优化

### 1. 原型方法优化

```javascript
// 优化前
function Person(name, age) {
    this.name = name;
    this.age = age;
    this.sayHello = function() {
        console.log(`你好，我是${this.name}`);
    };
}

// 优化后
function Person(name, age) {
    this.name = name;
    this.age = age;
}

Person.prototype.sayHello = function() {
    console.log(`你好，我是${this.name}`);
};
```

### 2. 属性描述符

```javascript
function Product(name, price) {
    // 定义不可变属性
    Object.defineProperties(this, {
        name: {
            value: name,
            writable: false,
            enumerable: true
        },
        price: {
            value: price,
            writable: true,
            enumerable: true
        }
    });
}

// 添加计算属性
Object.defineProperty(Product.prototype, 'priceWithTax', {
    get() {
        return this.price * 1.2;
    }
});
```

## 实践示例

### 1. 组件构造函数

```javascript
// UI组件构造函数
function Component(options) {
    this.element = options.element;
    this.data = options.data || {};
    this.template = options.template;
    
    // 初始化
    this.init();
}

Component.prototype.init = function() {
    this.render();
    this.bindEvents();
};

Component.prototype.render = function() {
    this.element.innerHTML = this.template(this.data);
};

Component.prototype.bindEvents = function() {
    // 事件绑定逻辑
};

// 使用示例
const button = new Component({
    element: document.querySelector('#button'),
    data: { text: '点击我' },
    template: data => `<button>${data.text}</button>`
});
```

### 2. 数据模型构造函数

```javascript
// 数据模型构造函数
function Model(attributes) {
    this.attributes = {};
    this.set(attributes);
}

Model.prototype.set = function(attributes) {
    Object.assign(this.attributes, attributes);
    this.validate();
};

Model.prototype.get = function(key) {
    return this.attributes[key];
};

Model.prototype.validate = function() {
    // 验证逻辑
};

// 使用示例
const user = new Model({
    name: '张三',
    email: 'zhangsan@example.com'
});
```

## 最佳实践

1. 命名约定
   ```javascript
   // 构造函数使用大写开头
   function User(name) {
       this.name = name;
   }
   
   // 普通函数使用小写开头
   function createUser(name) {
       return new User(name);
   }
   ```

2. 参数处理
   ```javascript
   function Person(options = {}) {
       // 使用解构赋值设置默认值
       const {
           name = '',
           age = 0,
           email = null
       } = options;
       
       this.name = name;
       this.age = age;
       this.email = email;
   }
   ```

3. 错误处理
   ```javascript
   function Account(balance) {
       if (!(this instanceof Account)) {
           throw new Error('必须使用new操作符');
       }
       
       if (typeof balance !== 'number') {
           throw new TypeError('余额必须是数字');
       }
       
       this.balance = balance;
   }
   ```

## 总结

- 掌握构造函数基础
- 理解原型和继承
- 使用构造函数模式
- 实现高级特性
- 优化构造函数
- 遵循最佳实践

下一章将介绍JavaScript事件。
