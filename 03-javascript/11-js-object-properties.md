---
title: "JavaScript对象属性"
slug: "javascript-object-properties"
sequence: 11
description: "详细介绍JavaScript对象属性的特性和操作方法"
is_published: true
estimated_minutes: 25
language: "zh-CN"
---

# JavaScript对象属性

## 属性类型

### 1. 数据属性

```javascript
// 基本数据属性
const person = {
    name: "张三",  // 数据属性
    age: 25       // 数据属性
};

// 使用属性描述符
Object.defineProperty(person, 'id', {
    value: 1001,           // 属性值
    writable: true,        // 是否可写
    enumerable: true,      // 是否可枚举
    configurable: true     // 是否可配置
});
```

### 2. 访问器属性

```javascript
const person = {
    firstName: '张',
    lastName: '三',
    // 访问器属性
    get fullName() {
        return this.firstName + this.lastName;
    },
    set fullName(name) {
        [this.firstName, this.lastName] = name.split('');
    }
};

// 使用属性描述符定义访问器
Object.defineProperty(person, 'age', {
    get() {
        return this._age;
    },
    set(value) {
        if (value < 0) {
            throw new Error('年龄不能为负数');
        }
        this._age = value;
    }
});
```

## 属性描述符

### 1. 数据属性描述符

```javascript
// 完整的数据属性描述符
const user = {};

Object.defineProperty(user, 'name', {
    value: '李四',         // 属性值
    writable: true,       // 是否可写
    enumerable: true,     // 是否可枚举
    configurable: true    // 是否可配置
});

// 只读属性
Object.defineProperty(user, 'id', {
    value: 1002,
    writable: false       // 设置为只读
});

// 不可枚举属性
Object.defineProperty(user, 'password', {
    value: '123456',
    enumerable: false     // 在循环中不可见
});
```

### 2. 访问器属性描述符

```javascript
const product = {
    _price: 0
};

Object.defineProperty(product, 'price', {
    get() {
        return this._price;
    },
    set(value) {
        if (value < 0) {
            throw new Error('价格不能为负数');
        }
        this._price = value;
    },
    enumerable: true,    // 是否可枚举
    configurable: true   // 是否可配置
});
```

## 属性操作

### 1. 属性检测

```javascript
const obj = {
    name: '王五',
    age: 30
};

// in 运算符
console.log('name' in obj);              // true
console.log('toString' in obj);          // true（继承属性）

// hasOwnProperty 方法
console.log(obj.hasOwnProperty('name')); // true
console.log(obj.hasOwnProperty('toString')); // false

// propertyIsEnumerable 方法
console.log(obj.propertyIsEnumerable('name')); // true
```

### 2. 属性枚举

```javascript
const person = {
    name: '赵六',
    age: 35
};

// Object.keys()
console.log(Object.keys(person));        // ['name', 'age']

// Object.values()
console.log(Object.values(person));      // ['赵六', 35]

// Object.entries()
console.log(Object.entries(person));     // [['name','赵六'], ['age',35]]

// Object.getOwnPropertyNames()
console.log(Object.getOwnPropertyNames(person)); // ['name', 'age']
```

### 3. 属性定义

```javascript
// 单个属性定义
Object.defineProperty(person, 'gender', {
    value: '男',
    writable: true,
    enumerable: true,
    configurable: true
});

// 多个属性定义
Object.defineProperties(person, {
    email: {
        value: 'example@email.com',
        writable: true
    },
    phone: {
        value: '123456789',
        writable: true
    }
});
```

## 属性继承

### 1. 原型属性

```javascript
function Person(name) {
    this.name = name;
}

Person.prototype.sayHello = function() {
    console.log(`Hello, I'm ${this.name}`);
};

const person1 = new Person('张三');
person1.sayHello(); // "Hello, I'm 张三"

// 检查原型属性
console.log(person1.hasOwnProperty('sayHello')); // false
console.log('sayHello' in person1); // true
```

### 2. 属性遮蔽

```javascript
function Animal(name) {
    this.name = name;
}

Animal.prototype.makeSound = function() {
    return '某种声音';
};

const cat = new Animal('猫');
// 遮蔽原型方法
cat.makeSound = function() {
    return '喵喵';
};

console.log(cat.makeSound()); // "喵喵"
```

## 属性特性

### 1. 可写性

```javascript
const config = {
    apiUrl: 'https://api.example.com'
};

// 设置只读属性
Object.defineProperty(config, 'apiUrl', {
    writable: false
});

// config.apiUrl = 'new-url'; // 错误：无法修改只读属性

// 批量设置只读属性
const settings = {
    theme: 'dark',
    language: 'zh-CN'
};

Object.keys(settings).forEach(key => {
    Object.defineProperty(settings, key, {
        writable: false
    });
});
```

### 2. 可枚举性

```javascript
const user = {
    name: '李四',
    password: '123456'
};

// 隐藏敏感属性
Object.defineProperty(user, 'password', {
    enumerable: false
});

// 遍历属性
for (let key in user) {
    console.log(key); // 只输出 "name"
}

// 获取所有属性（包括不可枚举）
console.log(Object.getOwnPropertyNames(user)); // ["name", "password"]
```

### 3. 可配置性

```javascript
const api = {
    url: 'https://api.example.com'
};

// 锁定属性配置
Object.defineProperty(api, 'url', {
    configurable: false
});

// 以下操作将抛出错误
// Object.defineProperty(api, 'url', {
//     writable: false
// });
// delete api.url;
```

## 实践示例

### 1. 数据验证

```javascript
function createValidatedObject() {
    const data = {
        _age: 0,
        _email: ''
    };
    
    Object.defineProperties(data, {
        age: {
            get() {
                return this._age;
            },
            set(value) {
                if (typeof value !== 'number') {
                    throw new TypeError('年龄必须是数字');
                }
                if (value < 0 || value > 150) {
                    throw new RangeError('年龄必须在0-150之间');
                }
                this._age = value;
            }
        },
        email: {
            get() {
                return this._email;
            },
            set(value) {
                if (!/\S+@\S+\.\S+/.test(value)) {
                    throw new Error('邮箱格式不正确');
                }
                this._email = value;
            }
        }
    });
    
    return data;
}
```

### 2. 计算属性

```javascript
function createCircle(radius) {
    const circle = {
        _radius: radius
    };
    
    Object.defineProperties(circle, {
        radius: {
            get() {
                return this._radius;
            },
            set(value) {
                if (value < 0) {
                    throw new Error('半径不能为负数');
                }
                this._radius = value;
            }
        },
        area: {
            get() {
                return Math.PI * this._radius ** 2;
            }
        },
        circumference: {
            get() {
                return 2 * Math.PI * this._radius;
            }
        }
    });
    
    return circle;
}
```

## 最佳实践

1. 属性命名
   ```javascript
   // 使用下划线前缀表示私有属性
   const user = {
       _password: '123456',
       get password() {
           throw new Error('密码不可访问');
       }
   };
   ```

2. 属性访问控制
   ```javascript
   // 使用闭包保护私有属性
   function createPerson(name) {
       let _name = name;
       
       return {
           getName() {
               return _name;
           },
           setName(value) {
               if (typeof value !== 'string') {
                   throw new TypeError('名字必须是字符串');
               }
               _name = value;
           }
       };
   }
   ```

3. 属性描述符使用
   ```javascript
   // 使用Object.defineProperties批量定义
   const product = {};
   
   Object.defineProperties(product, {
       name: {
           value: 'Product',
           writable: true,
           enumerable: true
       },
       price: {
           value: 100,
           writable: true,
           enumerable: true
       },
       id: {
           value: 'P001',
           writable: false,
           enumerable: false
       }
   });
   ```

## 总结

- 理解数据属性和访问器属性
- 掌握属性描述符的使用
- 了解属性操作方法
- 正确处理属性继承
- 合理使用属性特性
- 遵循最佳实践

下一章将介绍JavaScript对象方法。
