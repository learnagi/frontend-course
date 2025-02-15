---
title: "JavaScript字符串搜索"
slug: "javascript-string-search"
sequence: 18
description: "详细介绍JavaScript字符串搜索的方法和技巧"
is_published: true
estimated_minutes: 25
language: "zh-CN"
---

# JavaScript字符串搜索

## 基本搜索方法

### 1. indexOf 和 lastIndexOf

```javascript
const text = 'Hello World, Hello JavaScript';

// indexOf - 从前向后搜索
console.log(text.indexOf('Hello'));      // 0
console.log(text.indexOf('Hello', 1));   // 13 (从位置1开始搜索)
console.log(text.indexOf('Python'));     // -1 (未找到)

// lastIndexOf - 从后向前搜索
console.log(text.lastIndexOf('Hello'));  // 13
console.log(text.lastIndexOf('o'));      // 19
console.log(text.lastIndexOf('o', 18));  // 7 (从位置18开始向前搜索)
```

### 2. includes, startsWith, endsWith

```javascript
const str = 'Hello World';

// includes - 包含搜索
console.log(str.includes('World'));     // true
console.log(str.includes('World', 6));  // true (从位置6开始搜索)

// startsWith - 开始搜索
console.log(str.startsWith('Hello'));   // true
console.log(str.startsWith('World', 6)); // true

// endsWith - 结束搜索
console.log(str.endsWith('World'));     // true
console.log(str.endsWith('Hello', 5));  // true (检查前5个字符)
```

## 正则表达式搜索

### 1. search方法

```javascript
const text = 'Hello World 2025';

// 基本搜索
console.log(text.search('World'));      // 6

// 使用正则表达式
console.log(text.search(/\d+/));        // 12 (查找数字)
console.log(text.search(/world/i));     // 6 (忽略大小写)

// 未找到返回-1
console.log(text.search(/xyz/));        // -1
```

### 2. match和matchAll

```javascript
const text = 'Hello World, Hello JavaScript, Hello Python';

// match - 查找匹配项
const matches = text.match(/Hello/g);
console.log(matches);  // ["Hello", "Hello", "Hello"]

// matchAll - 查找所有匹配项及其详细信息
const regex = /Hello/g;
for (const match of text.matchAll(regex)) {
    console.log(match.index, match[0]);  // 输出每个匹配的位置和内容
}

// 使用捕获组
const dateStr = '2025-02-15';
const dateRegex = /(\d{4})-(\d{2})-(\d{2})/;
const dateMatch = dateStr.match(dateRegex);
console.log(dateMatch[1]);  // "2025"
console.log(dateMatch[2]);  // "02"
console.log(dateMatch[3]);  // "15"
```

## 高级搜索技巧

### 1. 模式匹配

```javascript
// 常用正则表达式模式
const patterns = {
    // 邮箱匹配
    email: /^[^\s@]+@[^\s@]+\.[^\s@]+$/,
    
    // URL匹配
    url: /^(https?:\/\/)?([\da-z.-]+)\.([a-z.]{2,6})([\/\w .-]*)*\/?$/,
    
    // 电话号码匹配
    phone: /^1[3-9]\d{9}$/,
    
    // 中文字符匹配
    chinese: /[\u4e00-\u9fa5]/,
    
    // 密码强度匹配（至少包含大小写字母、数字和特殊字符）
    strongPassword: /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[@$!%*?&])[A-Za-z\d@$!%*?&]{8,}$/
};

// 使用示例
function validatePattern(text, patternName) {
    return patterns[patternName].test(text);
}
```

### 2. 模糊搜索

```javascript
// 简单模糊搜索
function fuzzySearch(text, search) {
    const pattern = search
        .split('')
        .map(char => `${char}.*`)
        .join('');
    return new RegExp(pattern, 'i').test(text);
}

// 带评分的模糊搜索
function fuzzySearchWithScore(text, search) {
    const results = [];
    const searchLower = search.toLowerCase();
    const textLower = text.toLowerCase();
    
    let score = 0;
    let lastIndex = -1;
    
    // 计算匹配分数
    for (let i = 0; i < searchLower.length; i++) {
        const char = searchLower[i];
        const index = textLower.indexOf(char, lastIndex + 1);
        
        if (index === -1) {
            return null;
        }
        
        score += (index - lastIndex);
        lastIndex = index;
    }
    
    return {
        text,
        score: 1 / (1 + score)  // 分数越高表示匹配度越高
    };
}
```

## 搜索优化

### 1. 性能优化

```javascript
// 预编译正则表达式
const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;

function validateEmails(emails) {
    return emails.map(email => emailRegex.test(email));
}

// 使用字符串缓存
function searchWithCache(texts, pattern) {
    const cache = new Map();
    const regex = new RegExp(pattern);
    
    return texts.map(text => {
        if (cache.has(text)) {
            return cache.get(text);
        }
        
        const result = regex.test(text);
        cache.set(text, result);
        return result;
    });
}
```

### 2. 搜索结果高亮

```javascript
// 高亮搜索结果
function highlightText(text, search, highlightClass = 'highlight') {
    if (!search) return text;
    
    const regex = new RegExp(`(${search})`, 'gi');
    return text.replace(regex, `<span class="${highlightClass}">$1</span>`);
}

// 高亮多个关键词
function highlightMultipleKeywords(text, keywords, highlightClass = 'highlight') {
    if (!keywords.length) return text;
    
    const regex = new RegExp(`(${keywords.join('|')})`, 'gi');
    return text.replace(regex, `<span class="${highlightClass}">$1</span>`);
}
```

## 实践示例

### 1. 搜索引擎实现

```javascript
class SearchEngine {
    constructor(documents) {
        this.documents = documents;
        this.index = this.buildIndex();
    }
    
    // 建立倒排索引
    buildIndex() {
        const index = new Map();
        
        this.documents.forEach((doc, docId) => {
            const words = doc.toLowerCase().split(/\W+/);
            
            words.forEach(word => {
                if (!index.has(word)) {
                    index.set(word, new Set());
                }
                index.get(word).add(docId);
            });
        });
        
        return index;
    }
    
    // 搜索方法
    search(query) {
        const words = query.toLowerCase().split(/\W+/);
        const results = new Map();
        
        words.forEach(word => {
            const matchingDocs = this.index.get(word) || new Set();
            
            matchingDocs.forEach(docId => {
                results.set(docId, (results.get(docId) || 0) + 1);
            });
        });
        
        // 按匹配度排序
        return Array.from(results.entries())
            .sort((a, b) => b[1] - a[1])
            .map(([docId]) => this.documents[docId]);
    }
}
```

### 2. 自动完成实现

```javascript
class Autocomplete {
    constructor(dictionary) {
        this.dictionary = dictionary;
        this.trie = this.buildTrie();
    }
    
    // 建立Trie树
    buildTrie() {
        const root = {};
        
        this.dictionary.forEach(word => {
            let node = root;
            
            for (const char of word) {
                if (!node[char]) {
                    node[char] = {};
                }
                node = node[char];
            }
            
            node.isEnd = true;
            node.word = word;
        });
        
        return root;
    }
    
    // 搜索建议
    suggest(prefix) {
        let node = this.trie;
        const suggestions = [];
        
        // 找到前缀对应的节点
        for (const char of prefix) {
            if (!node[char]) {
                return suggestions;
            }
            node = node[char];
        }
        
        // 收集建议
        this.collectWords(node, suggestions);
        return suggestions;
    }
    
    // 递归收集单词
    collectWords(node, suggestions, limit = 10) {
        if (suggestions.length >= limit) {
            return;
        }
        
        if (node.isEnd) {
            suggestions.push(node.word);
        }
        
        for (const char in node) {
            if (char !== 'isEnd' && char !== 'word') {
                this.collectWords(node[char], suggestions, limit);
            }
        }
    }
}
```

## 最佳实践

1. 正则表达式使用
   ```javascript
   // 推荐：预编译正则表达式
   const EMAIL_REGEX = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
   
   // 推荐：使用命名捕获组
   const DATE_REGEX = /(?<year>\d{4})-(?<month>\d{2})-(?<day>\d{2})/;
   ```

2. 性能考虑
   ```javascript
   // 推荐：使用适当的搜索方法
   function findText(text, search) {
       // 简单搜索用indexOf
       if (search.length === 1) {
           return text.indexOf(search);
       }
       
       // 复杂搜索用正则表达式
       return text.search(new RegExp(search, 'i'));
   }
   ```

3. 错误处理
   ```javascript
   // 推荐：安全的搜索实现
   function safeSearch(text, pattern) {
       try {
           const regex = new RegExp(pattern);
           return regex.test(text);
       } catch (error) {
           console.error('无效的搜索模式:', error);
           return false;
       }
   }
   ```

## 总结

- 掌握基本搜索方法
- 熟练使用正则表达式
- 实现高级搜索功能
- 优化搜索性能
- 处理特殊情况
- 遵循最佳实践

下一章将介绍JavaScript字符串模板。
