---
title: "HTML属性"
slug: "html-attributes"
sequence: 6
description: "掌握HTML属性的使用方法，了解全局属性和自定义数据属性的应用"
is_published: true
estimated_minutes: 25
language: "zh-CN"
---

# HTML属性

![HTML属性](./images/html-attributes.png)
*掌握HTML属性，增强元素功能*

## 本节概要

通过本节学习，你将学会：
- 理解HTML属性的基本概念
- 掌握常用全局属性的使用
- 学习自定义数据属性的应用
- 了解属性的最佳实践

💡 重点内容：
- 属性语法规则
- 全局属性使用
- 自定义数据属性
- 属性值的格式

## 1. 属性基础

### 属性语法
```html
<标签名 属性名="属性值">内容</标签名>
<标签名 属性名='属性值'>内容</标签名>
<标签名 布尔属性>内容</标签名>
```

### 属性值规则
- 使用双引号或单引号包裹
- 某些属性可以省略引号（不推荐）
- 布尔属性可以只写属性名

## 2. 常用全局属性

### class和id
```html
<div class="container main">
    <p id="intro" class="text-large">段落内容</p>
</div>
```

### style和title
```html
<p style="color: blue; font-size: 16px;" title="这是一个提示">
    鼠标悬停查看提示文本
</p>
```

### lang和dir
```html
<p lang="zh-CN">中文内容</p>
<p lang="en" dir="ltr">English content</p>
<p lang="ar" dir="rtl">محتوى عربي</p>
```

## 3. 特定元素属性

### 图片属性
```html
<img src="image.jpg" 
     alt="图片描述" 
     width="300" 
     height="200"
     loading="lazy">
```

### 链接属性
```html
<a href="https://example.com" 
   target="_blank"
   rel="noopener noreferrer">
   外部链接
</a>
```

### 表单属性
```html
<input type="text"
       name="username"
       required
       placeholder="请输入用户名"
       maxlength="20"
       disabled>
```

## 4. 自定义数据属性

### 基本语法
```html
<div data-user-id="123"
     data-role="admin"
     data-last-login="2025-02-10">
    用户信息
</div>
```

### JavaScript访问
```javascript
const userDiv = document.querySelector('div');
const userId = userDiv.dataset.userId;
const role = userDiv.dataset.role;
```

## 5. 实战练习

创建一个产品展示卡片：

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <title>产品卡片</title>
    <style>
        .product-card {
            border: 1px solid #ddd;
            padding: 15px;
            max-width: 300px;
            margin: 20px;
        }
        
        .product-image {
            width: 100%;
            height: auto;
        }
        
        .product-title {
            color: #333;
            margin: 10px 0;
        }
        
        .product-price {
            color: #e44d26;
            font-weight: bold;
        }
        
        .product-button {
            background-color: #4CAF50;
            color: white;
            border: none;
            padding: 10px 20px;
            cursor: pointer;
        }
        
        .product-button[disabled] {
            background-color: #cccccc;
            cursor: not-allowed;
        }
    </style>
</head>
<body>
    <article class="product-card"
             data-product-id="12345"
             data-category="electronics"
             data-stock="5">
        
        <img class="product-image"
             src="product.jpg"
             alt="产品图片"
             loading="lazy">
        
        <h2 class="product-title"
            title="点击查看详情">
            智能手表
        </h2>
        
        <p class="product-price"
           data-currency="CNY">
            ¥999
        </p>
        
        <button class="product-button"
                type="button"
                onclick="addToCart()"
                aria-label="添加到购物车">
            加入购物车
        </button>
    </article>

    <script>
        function addToCart() {
            const card = document.querySelector('.product-card');
            const productId = card.dataset.productId;
            const stock = parseInt(card.dataset.stock);
            
            if (stock > 0) {
                alert(`添加商品 ${productId} 到购物车`);
                card.dataset.stock = stock - 1;
                
                if (stock - 1 === 0) {
                    const button = card.querySelector('.product-button');
                    button.disabled = true;
                    button.textContent = '已售罄';
                }
            }
        }
    </script>
</body>
</html>
```

## 6. 属性使用建议

1. 始终使用小写属性名
2. 始终为属性值加引号
3. 必要时使用布尔属性
4. 确保id值唯一
5. 适当使用自定义数据属性

## 7. 检查清单

- [ ] 属性名使用小写
- [ ] 属性值使用引号包裹
- [ ] 布尔属性格式正确
- [ ] ID值唯一
- [ ] 自定义数据属性以data-开头
- [ ] 属性值符合预期格式

## 下节预告

下一节：[HTML文本格式化](./07-html-text-formatting.md)
- 文本格式化标签
- 字体样式和大小
- 文本对齐和装饰
