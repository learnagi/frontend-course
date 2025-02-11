---
title: "HTML列表"
slug: "html-lists"
sequence: 16
description: "学习HTML列表的创建和使用，掌握内容组织的核心技术"
is_published: true
estimated_minutes: 25
language: "zh-CN"
---

# HTML列表

![HTML列表](./images/html-lists.png)
*使用HTML列表组织和展示内容*

## 本节概要

通过本节学习，你将学会：
- 创建有序和无序列表
- 使用定义列表
- 设置列表样式
- 创建嵌套列表

💡 重点内容：
- 列表的基本类型
- 列表的嵌套使用
- 列表样式定制
- 列表的最佳实践

## 1. 列表基础

### 无序列表
```html
<!-- 基本无序列表 -->
<ul>
    <li>苹果</li>
    <li>香蕉</li>
    <li>橙子</li>
</ul>

<!-- 带有自定义标记的无序列表 -->
<ul style="list-style-type: square">
    <li>新闻</li>
    <li>体育</li>
    <li>娱乐</li>
</ul>
```

### 有序列表
```html
<!-- 基本有序列表 -->
<ol>
    <li>第一步</li>
    <li>第二步</li>
    <li>第三步</li>
</ol>

<!-- 自定义编号类型的有序列表 -->
<ol type="A">
    <li>选项A</li>
    <li>选项B</li>
    <li>选项C</li>
</ol>
```

### 定义列表
```html
<dl>
    <dt>HTML</dt>
    <dd>超文本标记语言，用于创建网页结构</dd>
    
    <dt>CSS</dt>
    <dd>层叠样式表，用于设计网页样式</dd>
    
    <dt>JavaScript</dt>
    <dd>一种编程语言，用于实现网页交互</dd>
</dl>
```

## 2. 列表样式

### 基本样式
```css
/* 无序列表样式 */
ul {
    list-style-type: disc;    /* 实心圆 */
    padding-left: 20px;
    margin: 10px 0;
}

/* 有序列表样式 */
ol {
    list-style-type: decimal; /* 数字 */
    padding-left: 20px;
    margin: 10px 0;
}

/* 列表项样式 */
li {
    margin: 5px 0;
    line-height: 1.5;
}
```

### 自定义样式
```css
/* 自定义列表标记 */
ul.custom {
    list-style-type: none;
    padding: 0;
}

ul.custom li {
    padding-left: 20px;
    position: relative;
}

ul.custom li::before {
    content: "→";
    position: absolute;
    left: 0;
    color: #007bff;
}

/* 悬停效果 */
ul.custom li:hover::before {
    color: #0056b3;
    transform: translateX(5px);
    transition: all 0.3s ease;
}
```

## 3. 嵌套列表

### 基本嵌套
```html
<ul>
    <li>前端开发
        <ul>
            <li>HTML
                <ul>
                    <li>标签</li>
                    <li>属性</li>
                </ul>
            </li>
            <li>CSS
                <ul>
                    <li>选择器</li>
                    <li>样式</li>
                </ul>
            </li>
        </ul>
    </li>
    <li>后端开发
        <ul>
            <li>数据库</li>
            <li>服务器</li>
        </ul>
    </li>
</ul>
```

### 混合嵌套
```html
<ol>
    <li>学习路线
        <ul>
            <li>基础知识
                <ol type="a">
                    <li>HTML</li>
                    <li>CSS</li>
                    <li>JavaScript</li>
                </ol>
            </li>
            <li>进阶技能
                <ol type="a">
                    <li>框架</li>
                    <li>工具</li>
                </ol>
            </li>
        </ul>
    </li>
</ol>
```

## 4. 实际应用示例

### 导航菜单
```html
<nav>
    <ul class="nav-menu">
        <li><a href="#home">首页</a></li>
        <li><a href="#about">关于
            <ul class="submenu">
                <li><a href="#team">团队</a></li>
                <li><a href="#history">历史</a></li>
            </ul>
        </a></li>
        <li><a href="#contact">联系我们</a></li>
    </ul>
</nav>

<style>
.nav-menu {
    list-style: none;
    padding: 0;
    margin: 0;
    display: flex;
    background: #f8f9fa;
}

.nav-menu > li {
    position: relative;
    padding: 15px 20px;
}

.submenu {
    display: none;
    position: absolute;
    top: 100%;
    left: 0;
    background: white;
    box-shadow: 0 2px 5px rgba(0,0,0,0.1);
}

.nav-menu li:hover .submenu {
    display: block;
}
</style>
```

### 时间线
```html
<ul class="timeline">
    <li>
        <div class="time">2023</div>
        <div class="event">公司成立</div>
    </li>
    <li>
        <div class="time">2024</div>
        <div class="event">产品发布</div>
    </li>
</ul>

<style>
.timeline {
    list-style: none;
    padding: 0;
    position: relative;
}

.timeline::before {
    content: '';
    position: absolute;
    left: 50px;
    top: 0;
    bottom: 0;
    width: 2px;
    background: #ddd;
}

.timeline li {
    padding: 20px 0 20px 70px;
    position: relative;
}

.timeline .time {
    font-weight: bold;
    margin-bottom: 5px;
}

.timeline li::before {
    content: '';
    position: absolute;
    left: 44px;
    top: 24px;
    width: 12px;
    height: 12px;
    border-radius: 50%;
    background: #007bff;
    border: 2px solid white;
}
</style>
```

## 5. 最佳实践

### 设计建议
- 保持列表结构清晰
- 适当使用缩进
- 选择合适的列表类型
- 考虑移动设备显示效果

### 可访问性
```html
<!-- 使用适当的ARIA标签 -->
<ul role="list">
    <li role="listitem">列表项1</li>
    <li role="listitem">列表项2</li>
</ul>

<!-- 为导航列表添加描述 -->
<nav aria-label="主导航">
    <ul>
        <li><a href="#home">首页</a></li>
        <li><a href="#about">关于</a></li>
    </ul>
</nav>
```

### 性能优化
- 避免过深的嵌套
- 使用CSS控制样式而不是HTML属性
- 合理使用选择器
- 优化动画效果

## 练习
1. 创建一个多级导航菜单
2. 实现一个带有自定义样式的时间线
3. 设计一个FAQ列表

## 常见问题
- 列表缩进不一致
  - 检查padding和margin设置
  - 使用一致的单位
  - 考虑使用CSS重置

- 列表标记位置偏移
  - 调整list-style-position
  - 使用自定义标记
  - 检查文本对齐方式

## 扩展阅读
- [MDN Web Docs - Lists](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/ul)
- [CSS-Tricks - List Styling](https://css-tricks.com/almanac/properties/l/list-style/)
- [Web.dev - Lists Best Practices](https://web.dev/learn/html/lists/)
