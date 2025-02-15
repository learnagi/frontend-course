---
title: "JavaScript字符串模板"
slug: "javascript-string-template"
sequence: 19
description: "详细介绍JavaScript字符串模板的使用方法和高级特性"
is_published: true
estimated_minutes: 25
language: "zh-CN"
---

# JavaScript字符串模板

## 基础语法

### 1. 模板字符串

```javascript
// 基本语法
const name = '张三';
const age = 25;
const message = `我叫${name}，今年${age}岁`;

// 多行字符串
const html = `
    <div>
        <h1>标题</h1>
        <p>段落</p>
    </div>
`;

// 表达式计算
const price = 100;
const tax = 0.2;
const total = `总价：${price * (1 + tax)}`;
```

### 2. 嵌套模板

```javascript
const users = [
    { name: '张三', age: 25 },
    { name: '李四', age: 30 }
];

const template = `
    <ul>
        ${users.map(user => `
            <li>
                <span>${user.name}</span>
                <span>${user.age}</span>
            </li>
        `).join('')}
    </ul>
`;
```

## 标签模板

### 1. 基本标签函数

```javascript
// 简单标签函数
function simpleTag(strings, ...values) {
    let result = '';
    for (let i = 0; i < strings.length; i++) {
        result += strings[i];
        if (i < values.length) {
            result += values[i];
        }
    }
    return result;
}

const name = '张三';
const age = 25;
const result = simpleTag`我叫${name}，今年${age}岁`;

// 高亮标签函数
function highlight(strings, ...values) {
    let result = '';
    strings.forEach((str, i) => {
        result += str;
        if (i < values.length) {
            result += `<span class="highlight">${values[i]}</span>`;
        }
    });
    return result;
}

const highlightedText = highlight`重要提示：${message}`;
```

### 2. 高级标签函数

```javascript
// 安全HTML标签函数
function safeHtml(strings, ...values) {
    const escapeHtml = (str) => {
        return str
            .replace(/&/g, '&amp;')
            .replace(/</g, '&lt;')
            .replace(/>/g, '&gt;')
            .replace(/"/g, '&quot;')
            .replace(/'/g, '&#039;');
    };
    
    return strings.reduce((result, str, i) => {
        const value = values[i - 1];
        const safeValue = value instanceof SafeHtml 
            ? value.toString()
            : escapeHtml(String(value));
        return result + safeValue + str;
    });
}

// 国际化标签函数
function i18n(strings, ...values) {
    const translate = (key) => {
        // 假设这是翻译查找函数
        const translations = {
            'zh-CN': { hello: '你好' },
            'en-US': { hello: 'Hello' }
        };
        return translations[currentLocale][key] || key;
    };
    
    return strings.reduce((result, str, i) => {
        const value = values[i - 1];
        const translatedValue = translate(value);
        return result + translatedValue + str;
    });
}
```

## 模板引擎实现

### 1. 简单模板引擎

```javascript
class SimpleTemplate {
    static compile(template) {
        return function(data) {
            return template.replace(/\${(.*?)}/g, (match, key) => {
                return data[key.trim()] || '';
            });
        };
    }
    
    static render(template, data) {
        const compiled = this.compile(template);
        return compiled(data);
    }
}

// 使用示例
const template = '你好，${name}！今年${age}岁了。';
const data = { name: '张三', age: 25 };
console.log(SimpleTemplate.render(template, data));
```

### 2. 高级模板引擎

```javascript
class AdvancedTemplate {
    constructor(options = {}) {
        this.options = {
            openTag: '{{',
            closeTag: '}}',
            ...options
        };
        this.cache = new Map();
    }
    
    compile(template) {
        if (this.cache.has(template)) {
            return this.cache.get(template);
        }
        
        const tokens = this.parse(template);
        const renderFn = this.generate(tokens);
        this.cache.set(template, renderFn);
        
        return renderFn;
    }
    
    parse(template) {
        const tokens = [];
        const { openTag, closeTag } = this.options;
        let pos = 0;
        
        while (pos < template.length) {
            // 查找开始标记
            const openStart = template.indexOf(openTag, pos);
            
            if (openStart === -1) {
                tokens.push({
                    type: 'text',
                    value: template.slice(pos)
                });
                break;
            }
            
            // 添加文本标记
            if (openStart > pos) {
                tokens.push({
                    type: 'text',
                    value: template.slice(pos, openStart)
                });
            }
            
            // 查找结束标记
            const openEnd = openStart + openTag.length;
            const closeStart = template.indexOf(closeTag, openEnd);
            
            if (closeStart === -1) {
                throw new Error('未闭合的标签');
            }
            
            // 添加表达式标记
            const expr = template.slice(openEnd, closeStart).trim();
            tokens.push({
                type: 'expression',
                value: expr
            });
            
            pos = closeStart + closeTag.length;
        }
        
        return tokens;
    }
    
    generate(tokens) {
        const code = ['let result = "";'];
        
        tokens.forEach(token => {
            if (token.type === 'text') {
                code.push(`result += "${token.value}";`);
            } else if (token.type === 'expression') {
                code.push(`result += ${token.value};`);
            }
        });
        
        code.push('return result;');
        
        return new Function('data', code.join('\n'));
    }
    
    render(template, data) {
        const renderFn = this.compile(template);
        return renderFn.call(data, data);
    }
}
```

## 实践应用

### 1. HTML模板生成

```javascript
// 组件模板
class Component {
    constructor(props) {
        this.props = props;
    }
    
    template() {
        return `
            <div class="component">
                <h2>${this.props.title}</h2>
                <p>${this.props.content}</p>
            </div>
        `;
    }
    
    render() {
        return this.template();
    }
}

// 列表渲染
function renderList(items) {
    return `
        <ul class="list">
            ${items.map(item => `
                <li class="list-item">
                    <h3>${item.title}</h3>
                    <p>${item.description}</p>
                </li>
            `).join('')}
        </ul>
    `;
}
```

### 2. 动态SQL生成

```javascript
// SQL模板生成器
class SQLTemplate {
    static select(table, conditions = {}) {
        const where = Object.entries(conditions)
            .map(([key, value]) => `${key} = '${value}'`)
            .join(' AND ');
            
        return `
            SELECT * FROM ${table}
            ${where ? `WHERE ${where}` : ''}
        `;
    }
    
    static insert(table, data) {
        const columns = Object.keys(data).join(', ');
        const values = Object.values(data)
            .map(value => `'${value}'`)
            .join(', ');
            
        return `
            INSERT INTO ${table} (${columns})
            VALUES (${values})
        `;
    }
}
```

## 最佳实践

1. 模板字符串使用
   ```javascript
   // 推荐：使用模板字符串进行字符串拼接
   const name = '张三';
   const greeting = `你好，${name}！`;
   
   // 推荐：处理多行字符串
   const html = `
       <div>
           <h1>标题</h1>
           <p>内容</p>
       </div>
   `.trim();
   ```

2. 标签函数使用
   ```javascript
   // 推荐：创建可重用的标签函数
   function sanitize(strings, ...values) {
       const dirty = strings.reduce((prev, next, i) => {
           return prev + values[i - 1] + next;
       });
       return DOMPurify.sanitize(dirty);
   }
   ```

3. 性能优化
   ```javascript
   // 推荐：缓存编译后的模板
   const templateCache = new Map();
   
   function getTemplate(templateId) {
       if (!templateCache.has(templateId)) {
           const template = document.getElementById(templateId).innerHTML;
           templateCache.set(templateId, template);
       }
       return templateCache.get(templateId);
   }
   ```

## 总结

- 掌握模板字符串基础
- 理解标签模板功能
- 实现模板引擎
- 应用实践案例
- 遵循最佳实践
- 注意性能优化

下一章将介绍JavaScript数字。
