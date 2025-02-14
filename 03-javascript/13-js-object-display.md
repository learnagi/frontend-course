---
title: "JavaScript对象显示"
slug: "javascript-object-display"
sequence: 13
description: "详细介绍JavaScript对象的显示和转换方法"
is_published: true
estimated_minutes: 20
language: "zh-CN"
---

# JavaScript对象显示

## 对象转字符串

### 1. toString()方法

```javascript
// 默认toString()方法
const person = {
    name: '张三',
    age: 25
};
console.log(person.toString()); // "[object Object]"

// 自定义toString()方法
const book = {
    title: 'JavaScript教程',
    author: '李四',
    toString() {
        return `《${this.title}》 作者：${this.author}`;
    }
};
console.log(book.toString()); // "《JavaScript教程》 作者：李四"
```

### 2. valueOf()方法

```javascript
// 默认valueOf()方法
const counter = {
    count: 0,
    increment() {
        this.count++;
    }
};
console.log(counter.valueOf()); // {count: 0, increment: ƒ}

// 自定义valueOf()方法
const price = {
    value: 100,
    valueOf() {
        return this.value;
    }
};
console.log(+price); // 100
```

## JSON转换

### 1. JSON.stringify()

```javascript
// 基本使用
const user = {
    name: '王五',
    age: 30,
    city: '北京'
};
console.log(JSON.stringify(user));
// {"name":"王五","age":30,"city":"北京"}

// 格式化输出
console.log(JSON.stringify(user, null, 2));
/*
{
  "name": "王五",
  "age": 30,
  "city": "北京"
}
*/

// 自定义转换
const data = {
    name: '张三',
    birth: new Date('1990-01-01'),
    toString() {
        return `${this.name}的信息`;
    }
};
console.log(JSON.stringify(data));
// {"name":"张三","birth":"1990-01-01T00:00:00.000Z"}
```

### 2. toJSON()方法

```javascript
const event = {
    title: '会议',
    date: new Date('2025-01-01'),
    toJSON() {
        return {
            title: this.title,
            date: this.date.toISOString().split('T')[0]
        };
    }
};
console.log(JSON.stringify(event));
// {"title":"会议","date":"2025-01-01"}
```

## 对象显示方法

### 1. console方法

```javascript
const user = {
    name: '李四',
    age: 25,
    address: {
        city: '上海',
        street: '南京路'
    }
};

// 基本输出
console.log(user);

// 表格形式
console.table(user);

// 详细信息
console.dir(user);

// 自定义格式
console.log('%c用户信息', 'color: blue; font-weight: bold');
console.log(user);
```

### 2. 自定义显示

```javascript
class Product {
    constructor(name, price) {
        this.name = name;
        this.price = price;
    }
    
    // 自定义显示方法
    display() {
        return `商品：${this.name}，价格：￥${this.price}`;
    }
    
    // HTML显示方法
    toHTML() {
        return `
            <div class="product">
                <h3>${this.name}</h3>
                <p>￥${this.price}</p>
            </div>
        `;
    }
}

const product = new Product('手机', 1999);
console.log(product.display());
document.body.innerHTML += product.toHTML();
```

## 对象序列化

### 1. 基本序列化

```javascript
// 对象序列化
const data = {
    users: [
        { id: 1, name: '张三' },
        { id: 2, name: '李四' }
    ],
    timestamp: new Date()
};

// 序列化
const serialized = JSON.stringify(data);

// 反序列化
const deserialized = JSON.parse(serialized);
```

### 2. 自定义序列化

```javascript
class User {
    constructor(name, birthDate) {
        this.name = name;
        this.birthDate = new Date(birthDate);
    }
    
    // 自定义序列化
    serialize() {
        return {
            name: this.name,
            birthDate: this.birthDate.toISOString()
        };
    }
    
    // 自定义反序列化
    static deserialize(data) {
        return new User(
            data.name,
            new Date(data.birthDate)
        );
    }
}

const user = new User('张三', '1990-01-01');
const serialized = JSON.stringify(user.serialize());
const deserialized = User.deserialize(JSON.parse(serialized));
```

## 特殊情况处理

### 1. 循环引用

```javascript
// 处理循环引用
function decycle(obj) {
    const seen = new WeakSet();
    
    return JSON.stringify(obj, (key, value) => {
        if (typeof value === 'object' && value !== null) {
            if (seen.has(value)) {
                return '[Circular]';
            }
            seen.add(value);
        }
        return value;
    });
}

// 使用示例
const obj = { name: '张三' };
obj.self = obj;
console.log(decycle(obj));
// {"name":"张三","self":"[Circular]"}
```

### 2. 特殊类型

```javascript
// 处理特殊类型
function stringify(obj) {
    return JSON.stringify(obj, (key, value) => {
        if (value instanceof Map) {
            return {
                dataType: 'Map',
                value: Array.from(value.entries())
            };
        }
        if (value instanceof Set) {
            return {
                dataType: 'Set',
                value: Array.from(value.values())
            };
        }
        if (value instanceof RegExp) {
            return {
                dataType: 'RegExp',
                source: value.source,
                flags: value.flags
            };
        }
        return value;
    });
}

// 使用示例
const data = {
    map: new Map([['key', 'value']]),
    set: new Set([1, 2, 3]),
    regex: /pattern/gi
};
console.log(stringify(data));
```

## 实践示例

### 1. 对象打印工具

```javascript
class ObjectPrinter {
    static print(obj, options = {}) {
        const {
            depth = 2,
            colors = true,
            indent = 2
        } = options;
        
        function formatValue(value, level) {
            if (level > depth) return '...';
            
            if (typeof value === 'object' && value !== null) {
                return ObjectPrinter.stringify(value, level + 1);
            }
            
            return JSON.stringify(value);
        }
        
        return ObjectPrinter.stringify(obj, 1);
    }
    
    static stringify(obj, level) {
        if (Array.isArray(obj)) {
            const items = obj.map(item => 
                formatValue(item, level)
            ).join(', ');
            return `[${items}]`;
        }
        
        const entries = Object.entries(obj).map(([key, value]) =>
            `${key}: ${formatValue(value, level)}`
        ).join(',\n' + ' '.repeat(level * 2));
        
        return `{\n${entries}\n${' '.repeat((level - 1) * 2)}}`;
    }
}
```

### 2. 对象比较工具

```javascript
class ObjectComparer {
    static compare(obj1, obj2) {
        return {
            added: this.findAdded(obj1, obj2),
            removed: this.findRemoved(obj1, obj2),
            modified: this.findModified(obj1, obj2)
        };
    }
    
    static findAdded(obj1, obj2) {
        return Object.keys(obj2).filter(key => 
            !(key in obj1)
        );
    }
    
    static findRemoved(obj1, obj2) {
        return Object.keys(obj1).filter(key => 
            !(key in obj2)
        );
    }
    
    static findModified(obj1, obj2) {
        return Object.keys(obj1).filter(key => 
            key in obj2 && 
            obj1[key] !== obj2[key]
        );
    }
}
```

## 最佳实践

1. 显示格式化
   ```javascript
   // 使用模板字符串格式化输出
   class Person {
       constructor(name, age, city) {
           this.name = name;
           this.age = age;
           this.city = city;
       }
       
       toString() {
           return `
               姓名：${this.name}
               年龄：${this.age}
               城市：${this.city}
           `.trim();
       }
   }
   ```

2. 序列化处理
   ```javascript
   // 处理日期等特殊类型
   function safeStringify(obj) {
       return JSON.stringify(obj, (key, value) => {
           if (value instanceof Date) {
               return {
                   type: 'Date',
                   value: value.toISOString()
               };
           }
           return value;
       });
   }
   ```

3. 错误处理
   ```javascript
   // 安全的JSON解析
   function safeParse(str) {
       try {
           return {
               data: JSON.parse(str),
               error: null
           };
       } catch (err) {
           return {
               data: null,
               error: err.message
           };
       }
   }
   ```

## 总结

- 掌握对象转字符串方法
- 理解JSON转换机制
- 使用不同显示方法
- 处理对象序列化
- 解决特殊情况
- 遵循最佳实践

下一章将介绍JavaScript对象构造函数。
