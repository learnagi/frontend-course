# ECMAScript 6 教程笔记

## 前言

ECMAScript 6（简称ES6）是JavaScript语言的下一代标准。它的目标是使JavaScript语言可以用来编写复杂的大型应用程序，成为企业级开发语言。

## ECMAScript 6 简介

### 什么是 ECMAScript 6
- ECMAScript 6 是 JavaScript 语言的新版本标准
- 2015年6月正式发布，又称 ES2015
- 目前主流浏览器都支持 ES6

### 主要特性
1. 声明变量的新方式（let、const）
2. 模板字符串
3. 解构赋值
4. 箭头函数
5. 类和模块
6. Promise
7. 新的数据结构（Set、Map）

## let 和 const 命令

### let 命令
```javascript
// let声明的变量只在其所在的代码块有效
{
  let a = 10;
  var b = 1;
}
a // ReferenceError: a is not defined
b // 1
```

特点：
1. 不存在变量提升
2. 暂时性死区
3. 不允许重复声明
4. 块级作用域

### const 命令
```javascript
const PI = 3.1415;
PI = 3; // TypeError: Assignment to constant variable
```

特点：
1. 声明常量，值不能改变
2. 必须立即初始化
3. 块级作用域
4. 对于复合类型，指向的地址不能改变

## 变量的解构赋值

### 数组的解构赋值
```javascript
let [a, b, c] = [1, 2, 3];
// a = 1
// b = 2
// c = 3
```

### 对象的解构赋值
```javascript
let { foo, bar } = { foo: 'aaa', bar: 'bbb' };
// foo = "aaa"
// bar = "bbb"
```

### 字符串的解构赋值
```javascript
const [a, b, c, d, e] = 'hello';
// a = "h"
// b = "e"
// c = "l"
// d = "l"
// e = "o"
```

## 字符串的扩展

### 模板字符串
```javascript
let name = 'Bob';
let time = 'today';
`Hello ${name}, how are you ${time}?`
// "Hello Bob, how are you today?"
```

### 新增方法
- includes()：返回布尔值，表示是否找到了参数字符串
- startsWith()：返回布尔值，表示参数字符串是否在源字符串的头部
- endsWith()：返回布尔值，表示参数字符串是否在源字符串的尾部

## 函数的扩展

### 箭头函数
```javascript
const sum = (a, b) => a + b;
// 等同于
const sum = function(a, b) {
  return a + b;
};
```

特点：
1. 更简洁的函数写法
2. 不绑定this
3. 不可以当作构造函数
4. 不可以使用arguments对象

### 函数参数的默认值
```javascript
function log(x, y = 'World') {
  console.log(x, y);
}
```

## Promise 对象

### 基本用法
```javascript
const promise = new Promise(function(resolve, reject) {
  // ... some code
  if (/* 异步操作成功 */){
    resolve(value);
  } else {
    reject(error);
  }
});
```

### Promise 链式调用
```javascript
promise
  .then(result => {/*...*/})
  .catch(error => {/*...*/})
  .finally(() => {/*...*/});
```

## Class 的基本语法

### 类的定义
```javascript
class Point {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  toString() {
    return '(' + this.x + ', ' + this.y + ')';
  }
}
```

### 类的继承
```javascript
class ColorPoint extends Point {
  constructor(x, y, color) {
    super(x, y); // 调用父类的constructor(x, y)
    this.color = color;
  }

  toString() {
    return this.color + ' ' + super.toString(); // 调用父类的toString()
  }
}
```

## Module 的语法

### export命令
```javascript
// profile.js
export var firstName = 'Michael';
export var lastName = 'Jackson';
export var year = 1958;
```

### import命令
```javascript
// main.js
import { firstName, lastName, year } from './profile.js';
```

## 数组的扩展

### 扩展运算符
```javascript
// 展开数组
const numbers = [1, 2, 3];
console.log(...numbers); // 1 2 3

// 合并数组
const array1 = [1, 2];
const array2 = [3, 4];
const combined = [...array1, ...array2]; // [1, 2, 3, 4]
```

### 新增数组方法
```javascript
// Array.from() - 将类数组对象转换为真正的数组
const arrayLike = document.querySelectorAll('div');
const divArray = Array.from(arrayLike);

// find() - 找到第一个满足条件的元素
const numbers = [1, 2, 3, 4, 5];
const found = numbers.find(num => num > 3); // 4

// findIndex() - 找到第一个满足条件的元素的索引
const index = numbers.findIndex(num => num > 3); // 3

// includes() - 判断数组是否包含某个值
const includes = numbers.includes(2); // true
```

## 对象的扩展

### 属性的简洁表示
```javascript
const name = 'Alice';
const age = 20;
// 属性名与变量名相同时，可以简写
const person = { name, age };
// 等同于 { name: name, age: age }
```

### 方法的简写
```javascript
const obj = {
  sayHi() {
    return 'Hello!';
  }
  // 等同于 sayHi: function() { return 'Hello!'; }
};
```

### 属性名表达式
```javascript
const propKey = 'foo';
const obj = {
  [propKey]: true,
  ['a' + 'bc']: 123
};
```

## Symbol

### 基本用法
```javascript
// Symbol 是一种新的原始数据类型，表示独一无二的值
const s1 = Symbol();
const s2 = Symbol('foo');
const s3 = Symbol('foo');
console.log(s2 === s3); // false

// 作为对象属性名
const mySymbol = Symbol();
const obj = {
  [mySymbol]: 'Hello!'
};
console.log(obj[mySymbol]); // 'Hello!'
```

### Symbol.for() 和 Symbol.keyFor()
```javascript
// Symbol.for() 会检查给定的key是否已经存在
const s1 = Symbol.for('foo');
const s2 = Symbol.for('foo');
console.log(s1 === s2); // true

// Symbol.keyFor() 返回一个已登记的Symbol类型值的key
console.log(Symbol.keyFor(s1)); // 'foo'
```

## Set 和 Map 数据结构

### Set
```javascript
// Set是一种新的数据结构，类似于数组，但成员值都是唯一的
const set = new Set([1, 2, 3, 4, 4]);
console.log(set.size); // 4

// 常用方法
set.add(5);
set.delete(2);
set.has(1);
set.clear();

// 数组去重
const array = [1, 2, 2, 3, 3, 4];
const unique = [...new Set(array)]; // [1, 2, 3, 4]
```

### Map
```javascript
// Map类似于对象，但是键可以是任何类型
const map = new Map();
const obj = { name: 'Alice' };

map.set(obj, 'data');
console.log(map.get(obj)); // 'data'

// 遍历方法
for (let [key, value] of map) {
  console.log(key, value);
}
```

## 异步编程的改进

### async/await
```javascript
async function fetchData() {
  try {
    const response = await fetch('https://api.example.com/data');
    const data = await response.json();
    return data;
  } catch (error) {
    console.error('Error:', error);
  }
}
```

### Generator 函数
```javascript
function* generateNumbers() {
  yield 1;
  yield 2;
  yield 3;
}

const gen = generateNumbers();
console.log(gen.next().value); // 1
console.log(gen.next().value); // 2
console.log(gen.next().value); // 3
```

## 最新提案

ES6之后，JavaScript语言的发展变得更加规范和开放。每年都会有新的特性被提出和添加，主要通过以下阶段：

- Stage 0 - Strawman（展示阶段）
- Stage 1 - Proposal（征求意见阶段）
- Stage 2 - Draft（草案阶段）
- Stage 3 - Candidate（候选阶段）
- Stage 4 - Finished（定案阶段）

## 编程风格建议

1. 块级作用域
   - let 取代 var
   - 全局常量和线程安全
   - const 优先，let 次之

2. 字符串
   - 静态字符串一律使用单引号或反引号
   - 动态字符串使用反引号

3. 解构赋值
   - 使用数组成员对变量赋值时，优先使用解构赋值
   - 函数的参数如果是对象的成员，优先使用解构赋值

4. 对象
   - 单行定义的对象，最后一个成员不以逗号结尾
   - 多行定义的对象，最后一个成员以逗号结尾

5. 函数
   - 立即执行函数可以写成箭头函数的形式
   - 那些使用匿名函数当作参数的场合，尽量用箭头函数代替
   - 箭头函数取代Function.prototype.bind
   - 简单的、单行的、不会复用的函数，建议采用箭头函数

## Proxy 和 Reflect

### Proxy
```javascript
// Proxy 用于创建一个对象的代理，从而实现基本操作的拦截和自定义
const handler = {
  get: function(target, prop) {
    return prop in target ? target[prop] : '属性不存在';
  },
  set: function(target, prop, value) {
    if (prop === 'age') {
      if (!Number.isInteger(value)) {
        throw new TypeError('年龄必须是整数');
      }
      if (value < 0) {
        throw new RangeError('年龄不能为负数');
      }
    }
    target[prop] = value;
    return true;
  }
};

const person = new Proxy({}, handler);
person.age = 25; // 正常设置
// person.age = -1; // 抛出 RangeError
console.log(person.name); // "属性不存在"
```

### Reflect
```javascript
// Reflect 是一个内置对象，提供拦截 JavaScript 操作的方法
// 1. 替代掉Object上的一些方法
const obj = {};
// 旧写法
'assign' in Object // true
// 新写法
Reflect.has(Object, 'assign') // true

// 2. 更优雅的方式操作对象
const target = {
  name: 'Alice',
  age: 25
};

// 获取属性
console.log(Reflect.get(target, 'name')); // 'Alice'

// 设置属性
Reflect.set(target, 'age', 26);

// 删除属性
Reflect.deleteProperty(target, 'age');

// 检查属性是否存在
console.log(Reflect.has(target, 'name')); // true
```

## 装饰器（Decorators）

```javascript
// 类装饰器
function readonly(target) {
  target.prototype.readonly = true;
}

@readonly
class Example {
  // ...
}

// 方法装饰器
function log(target, name, descriptor) {
  const original = descriptor.value;
  descriptor.value = function(...args) {
    console.log(`调用方法 ${name} 参数:`, args);
    return original.apply(this, args);
  };
  return descriptor;
}

class Math {
  @log
  add(a, b) {
    return a + b;
  }
}
```

## 模块化编程最佳实践

### 导出模块的推荐方式
```javascript
// math.js
// 1. 命名导出
export const add = (a, b) => a + b;
export const subtract = (a, b) => a - b;

// 2. 默认导出
export default class Calculator {
  // ...
}

// 3. 混合导出
export { add, subtract };
export default Calculator;
```

### 导入模块的推荐方式
```javascript
// 1. 导入特定的导出
import { add, subtract } from './math.js';

// 2. 导入默认导出
import Calculator from './math.js';

// 3. 导入所有导出
import * as MathUtils from './math.js';

// 4. 重命名导入
import { add as mathAdd } from './math.js';
```

## 实用的编程技巧

### 解构赋值的高级用法
```javascript
// 1. 提取JSON数据
const json = '{"name": "Alice", "age": 25}';
const { name, age } = JSON.parse(json);

// 2. 函数参数的默认值
function fetchData({ url, method = 'GET', headers = {} } = {}) {
  // ...
}

// 3. 交换变量
let x = 1, y = 2;
[x, y] = [y, x];
```

### 使用新的数组方法
```javascript
// 1. 数组去重并排序
const numbers = [3, 1, 2, 3, 4, 1];
const uniqueSorted = [...new Set(numbers)].sort((a, b) => a - b);

// 2. 扁平化数组
const nested = [1, [2, 3], [4, [5, 6]]];
const flattened = nested.flat(2); // [1, 2, 3, 4, 5, 6]

// 3. 数组元素过滤和转换
const numbers = [1, 2, 3, 4, 5];
const evenDoubled = numbers
  .filter(n => n % 2 === 0)
  .map(n => n * 2); // [4, 8]
```

### Promise的高级用法
```javascript
// 1. Promise.all 并行执行多个Promise
const promises = [
  fetch('/api/users'),
  fetch('/api/posts'),
  fetch('/api/comments')
];

Promise.all(promises)
  .then(([users, posts, comments]) => {
    // 处理所有响应
  })
  .catch(error => {
    // 处理任何错误
  });

// 2. Promise.race 竞态
const timeout = new Promise((_, reject) => 
  setTimeout(() => reject(new Error('超时')), 5000)
);

Promise.race([fetch('/api/data'), timeout])
  .then(response => {
    // 处理响应
  })
  .catch(error => {
    // 处理错误或超时
  });
```

## 性能优化建议

1. 使用 const 和 let 代替 var
   - 更好的作用域控制
   - 避免变量提升带来的问题
   - 防止意外修改变量

2. 使用箭头函数注意事项
   - 简单的单行返回值使用简写形式
   - 需要this绑定时使用普通函数
   - 事件处理器优先使用普通函数

3. 异步操作的最佳实践
   - 优先使用 async/await 而不是 Promise 链
   - 正确处理错误（try/catch）
   - 避免回调地狱

4. 模块化原则
   - 单一职责原则
   - 明确的导入/导出接口
   - 避免循环依赖

## 调试技巧

### 使用新的调试方法
```javascript
// 1. 对象的调试
const obj = { name: 'Alice', age: 25 };
console.log({ obj }); // { obj: { name: 'Alice', age: 25 } }

// 2. 使用断言
console.assert(obj.age >= 18, '年龄必须大于等于18岁');

// 3. 计时功能
console.time('循环时间');
for(let i = 0; i < 1000000; i++) {}
console.timeEnd('循环时间');

// 4. 跟踪调用栈
console.trace('跟踪调用');
```

## 正则的扩展

### RegExp 构造函数
```javascript
const regex = new RegExp('xyz', 'i');
const regex2 = new RegExp(/xyz/i);
```

### 新增特性
- `RegExp.prototype.flags`：返回正则表达式的修饰符
- `s` 修饰符：使 `.` 可以匹配任意字符
- 具名组匹配：为组匹配指定名字
- 后行断言：`(?<=y)x` 和 `(?<!y)x`

## 数值的扩展

### 二进制和八进制表示法
```javascript
// 二进制
0b111110111 === 503
// 八进制
0o767 === 503
```

### 新增方法
- `Number.isFinite()`：检查一个数值是否为有限的
- `Number.isNaN()`：检查一个值是否为 NaN
- `Number.parseInt()`：将字符串转为整数
- `Number.parseFloat()`：将字符串转为浮点数
- `Number.isInteger()`：判断一个数值是否为整数

## 对象的扩展

### 属性的简洁表示法
```javascript
const foo = 'bar';
const obj = {
  foo,  // 等同于 foo: foo
  method() {  // 等同于 method: function()
    return "Hello!";
  }
};
```

### 属性名表达式
```javascript
let propKey = 'foo';
let obj = {
  [propKey]: true,
  ['a' + 'bc']: 123
};
```

### 对象的新增方法

#### Object.assign()
```javascript
const target = { a: 1 };
const source1 = { b: 2 };
const source2 = { c: 3 };
Object.assign(target, source1, source2);
// target = { a: 1, b: 2, c: 3 }
```

#### Object.keys()、Object.values()、Object.entries()
```javascript
const obj = { foo: 'bar', baz: 42 };
Object.keys(obj);    // ['foo', 'baz']
Object.values(obj);  // ['bar', 42]
Object.entries(obj); // [['foo', 'bar'], ['baz', 42]]
```

## 运算符的扩展

### 指数运算符
```javascript
2 ** 3 // 8
let a = 2;
a **= 3; // 8
```

### 链判断运算符
```javascript
const obj = {
  foo: {
    bar: {
      baz: 42
    }
  }
};
const baz = obj?.foo?.bar?.baz; // 42
```

### Null 判断运算符
```javascript
const foo = null ?? 'default string';
// 'default string'
```

## Symbol

### 基本用法
```javascript
const s = Symbol();
const s1 = Symbol('foo');
const s2 = Symbol('foo');
s1 === s2 // false
```

### Symbol.for()、Symbol.keyFor()
```javascript
const s1 = Symbol.for('foo');
const s2 = Symbol.for('foo');
s1 === s2 // true

Symbol.keyFor(s1) // "foo"
```

## Set 和 Map 数据结构

### Set
```javascript
const s = new Set();
[2, 3, 5, 4, 5, 2, 2].forEach(x => s.add(x));
// Set结构 {2, 3, 5, 4}
```

### Map
```javascript
const m = new Map();
const o = {p: 'Hello World'};
m.set(o, 'content')
m.get(o) // "content"
```

## Proxy

### 基本用法
```javascript
const obj = new Proxy({}, {
  get: function (target, propKey, receiver) {
    console.log(`getting ${propKey}!`);
    return Reflect.get(target, propKey, receiver);
  },
  set: function (target, propKey, value, receiver) {
    console.log(`setting ${propKey}!`);
    return Reflect.set(target, propKey, value, receiver);
  }
});
```

## Reflect

### 静态方法
```javascript
// 查找并调用对象的方法
Reflect.get(target, name, receiver)
Reflect.set(target, name, value, receiver)
Reflect.has(target, name)
Reflect.deleteProperty(target, name)
Reflect.construct(target, args)
Reflect.getPrototypeOf(target)
Reflect.setPrototypeOf(target, prototype)
```

## Iterator 和 for...of 循环

### Iterator 接口
```javascript
const arr = ['a', 'b', 'c'];
const iter = arr[Symbol.iterator]();

iter.next() // { value: 'a', done: false }
iter.next() // { value: 'b', done: false }
iter.next() // { value: 'c', done: false }
iter.next() // { value: undefined, done: true }
```

### for...of 循环
```javascript
const arr = ['red', 'green', 'blue'];
for (let v of arr) {
  console.log(v);
}
```

## Generator 函数的语法

### 基本用法
```javascript
function* helloWorldGenerator() {
  yield 'hello';
  yield 'world';
  return 'ending';
}

const hw = helloWorldGenerator();
hw.next() // { value: 'hello', done: false }
hw.next() // { value: 'world', done: false }
hw.next() // { value: 'ending', done: true }
```

## Generator 函数的异步应用

### 异步操作的同步化表达
```javascript
function* loadUI() {
  showLoadingScreen();
  yield loadUIDataAsynchronously();
  hideLoadingScreen();
}
```

## async 函数

### 基本用法
```javascript
async function getStockPriceByName(name) {
  const symbol = await getStockSymbol(name);
  const stockPrice = await getStockPrice(symbol);
  return stockPrice;
}
```

### 错误处理
```javascript
async function f() {
  try {
    await Promise.reject('出错了');
  } catch(e) {
    console.log(e);
  }
}
```

## 异步遍历器

### for await...of
```javascript
async function* gen() {
  yield 'hello';
  yield 'world';
}

(async function() {
  for await (const x of gen()) {
    console.log(x);
  }
})();
```

## ArrayBuffer

### 基本用法
```javascript
// 创建一个16字节的缓冲区
const buffer = new ArrayBuffer(16);

// 创建一个指向buffer的Int32视图，开始于字节0，直到缓冲区的末尾
const int32View = new Int32Array(buffer);
```

## 最新提案

### 装饰器（Decorator）
```javascript
@testable
class MyTestableClass {
  // ...
}

function testable(target) {
  target.isTestable = true;
}
```

### 管道运算符
```javascript
// 提案阶段
let result = "hello"
  |> doubleSay
  |> capitalize
  |> exclaim;
```

### do 表达式
```javascript
// 提案阶段
let x = do {
  let t = f();
  t * t + 1;
};
```

## 编程风格

### 块级作用域
- 使用 `let` 取代 `var`
- 在 `let` 和 `const` 之间，优先使用 `const`

### 字符串
- 静态字符串一律使用单引号或反引号，不使用双引号
- 动态字符串使用反引号

### 解构赋值
- 使用数组成员对变量赋值时，优先使用解构赋值
- 函数的参数如果是对象的成员，优先使用解构赋值

### 对象
- 单行定义的对象，最后一个成员不以逗号结尾
- 多行定义的对象，最后一个成员以逗号结尾

### 函数
- 立即执行函数必须使用圆括号包起来
- 不要在函数体内使用 arguments 变量，使用 rest 运算符（...）代替

## 读懂规格

ECMAScript 的规格文件是计算机语言的标准，是对语言实现的详细描述。了解规格有助于：

1. 理解语言的底层实现
2. 发现语言的一些边界特性
3. 准确理解语言的各种特性

主要内容包括：
- 语言文法
- 类型系统
- 语义规则
- 运行时行为