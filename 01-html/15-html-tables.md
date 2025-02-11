---
title: "HTML表格"
slug: "html-tables"
sequence: 15
description: "学习HTML表格的创建和使用，掌握数据展示的核心技术"
is_published: true
estimated_minutes: 35
language: "zh-CN"
---

# HTML表格

![HTML表格](./images/html-tables.png)
*使用HTML表格组织和展示数据*

## 本节概要

通过本节学习，你将学会：
- 创建基本的HTML表格
- 设置表格的结构和样式
- 使用表格的高级特性
- 实现响应式表格设计

💡 重点内容：
- 表格的基本结构
- 单元格合并
- 表格样式设置
- 响应式表格技术

## 1. 表格基础

### 基本结构
```html
<table>
    <thead>
        <tr>
            <th>表头1</th>
            <th>表头2</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>数据1</td>
            <td>数据2</td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td>脚注1</td>
            <td>脚注2</td>
        </tr>
    </tfoot>
</table>
```

### 表格标签说明
- `<table>`: 定义表格
- `<thead>`: 表格头部
- `<tbody>`: 表格主体
- `<tfoot>`: 表格脚注
- `<tr>`: 表格行
- `<th>`: 表头单元格
- `<td>`: 数据单元格

## 2. 单元格合并

### 跨列合并
```html
<table>
    <tr>
        <td colspan="2">跨两列的单元格</td>
    </tr>
    <tr>
        <td>普通单元格</td>
        <td>普通单元格</td>
    </tr>
</table>
```

### 跨行合并
```html
<table>
    <tr>
        <td rowspan="2">跨两行的单元格</td>
        <td>第一行</td>
    </tr>
    <tr>
        <td>第二行</td>
    </tr>
</table>
```

## 3. 表格样式

### 基本样式
```css
table {
    width: 100%;
    border-collapse: collapse;
    margin: 20px 0;
}

th, td {
    padding: 12px;
    text-align: left;
    border: 1px solid #ddd;
}

th {
    background-color: #f5f5f5;
    font-weight: bold;
}

tr:nth-child(even) {
    background-color: #f9f9f9;
}

tr:hover {
    background-color: #f5f5f5;
}
```

### 响应式表格
```css
/* 响应式容器 */
.table-responsive {
    overflow-x: auto;
    -webkit-overflow-scrolling: touch;
}

/* 在小屏幕上的样式 */
@media screen and (max-width: 600px) {
    table {
        display: block;
        width: 100%;
    }
    
    thead {
        display: none;
    }
    
    tr {
        margin-bottom: 15px;
        display: block;
        border: 1px solid #ddd;
    }
    
    td {
        display: block;
        text-align: right;
        padding-left: 50%;
        position: relative;
    }
    
    td::before {
        content: attr(data-label);
        position: absolute;
        left: 0;
        width: 50%;
        padding-left: 15px;
        font-weight: bold;
        text-align: left;
    }
}
```

## 4. 高级特性

### 表格标题
```html
<table>
    <caption>员工信息表</caption>
    <tr>
        <th>姓名</th>
        <th>职位</th>
    </tr>
    <tr>
        <td>张三</td>
        <td>工程师</td>
    </tr>
</table>
```

### 列组
```html
<table>
    <colgroup>
        <col style="background-color: #f5f5f5">
        <col span="2" style="background-color: #fff">
    </colgroup>
    <tr>
        <th>产品</th>
        <th>价格</th>
        <th>库存</th>
    </tr>
    <tr>
        <td>商品A</td>
        <td>￥100</td>
        <td>50</td>
    </tr>
</table>
```

## 5. 实际应用示例

### 价格表
```html
<table class="pricing-table">
    <thead>
        <tr>
            <th>套餐</th>
            <th>基础版</th>
            <th>专业版</th>
            <th>企业版</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>价格</td>
            <td>￥99/月</td>
            <td>￥199/月</td>
            <td>￥399/月</td>
        </tr>
        <tr>
            <td>用户数</td>
            <td>5</td>
            <td>20</td>
            <td>无限</td>
        </tr>
        <tr>
            <td>存储空间</td>
            <td>10GB</td>
            <td>100GB</td>
            <td>1TB</td>
        </tr>
    </tbody>
</table>
```

### 时间表
```html
<table class="schedule-table">
    <thead>
        <tr>
            <th>时间</th>
            <th>周一</th>
            <th>周二</th>
            <th>周三</th>
            <th>周四</th>
            <th>周五</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>09:00</td>
            <td>会议</td>
            <td>培训</td>
            <td>开发</td>
            <td>测试</td>
            <td>部署</td>
        </tr>
        <tr>
            <td>14:00</td>
            <td>开发</td>
            <td>会议</td>
            <td>测试</td>
            <td>培训</td>
            <td>总结</td>
        </tr>
    </tbody>
</table>
```

## 6. 最佳实践

### 设计建议
- 保持表格结构简单清晰
- 适当使用表头和表尾
- 考虑移动设备的显示效果
- 使用适当的间距和边框

### 性能优化
- 避免过多的嵌套表格
- 使用CSS控制样式而不是HTML属性
- 考虑使用`<thead>`固定表头
- 大型表格考虑分页显示

### 可访问性
```html
<table>
    <caption>产品库存表</caption>
    <thead>
        <tr>
            <th scope="col">产品名称</th>
            <th scope="col">库存数量</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <th scope="row">商品A</th>
            <td>100</td>
        </tr>
    </tbody>
</table>
```

## 练习
1. 创建一个响应式的课程表
2. 实现一个带有合并单元格的组织架构图
3. 设计一个产品比较表

## 常见问题
- 表格不对齐
  - 检查单元格内容是否一致
  - 使用适当的padding和margin
  - 设置固定的列宽

- 响应式问题
  - 使用overflow-x: auto
  - 考虑在小屏幕上改变显示方式
  - 使用适当的媒体查询

## 扩展阅读
- [MDN Web Docs - Table](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/table)
- [CSS-Tricks - Complete Guide to Tables](https://css-tricks.com/complete-guide-table-element/)
- [响应式表格设计](https://www.w3schools.com/howto/howto_css_table_responsive.asp)
