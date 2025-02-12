---
title: "CSS预处理器和后处理器"
slug: "css-preprocessors-postprocessors"
sequence: 15
description: "掌握CSS预处理器和后处理器的使用方法"
is_published: true
estimated_minutes: 40
language: "zh-CN"
---

# CSS预处理器和后处理器

## CSS预处理器

### 1. Sass/SCSS

```scss
// 变量
$primary-color: #3498db;
$spacing: 20px;

// 嵌套规则
.container {
    max-width: 1200px;
    padding: $spacing;
    
    .header {
        background: $primary-color;
        
        &:hover {
            opacity: 0.9;
        }
    }
}

// 混合宏
@mixin flex-center {
    display: flex;
    justify-content: center;
    align-items: center;
}

.centered-box {
    @include flex-center;
}

// 函数
@function calculate-width($n) {
    @return $n * 100px;
}

.element {
    width: calculate-width(3);
}

// 继承
%button-base {
    padding: 10px 20px;
    border: none;
    border-radius: 4px;
}

.primary-button {
    @extend %button-base;
    background: $primary-color;
}
```

### 2. Less

```less
// 变量
@primary-color: #3498db;
@spacing: 20px;

// 混合
.flex-center() {
    display: flex;
    justify-content: center;
    align-items: center;
}

// 嵌套和&符号
.container {
    max-width: 1200px;
    padding: @spacing;
    
    &__header {
        background: @primary-color;
        
        &:hover {
            opacity: 0.9;
        }
    }
}

// 运算
.element {
    width: (100px * 3);
}

// 命名空间
#utils {
    .border(@color) {
        border: 1px solid @color;
    }
}

.box {
    #utils.border(@primary-color);
}
```

### 3. Stylus

```stylus
// 变量
primary-color = #3498db
spacing = 20px

// 混合
flex-center()
    display: flex
    justify-content: center
    align-items: center

// 嵌套
.container
    max-width: 1200px
    padding: spacing
    
    .header
        background: primary-color
        
        &:hover
            opacity: 0.9

// 函数
calculate-width(n)
    return n * 100px

.element
    width: calculate-width(3)
```

## CSS后处理器

### 1. PostCSS

```css
/* autoprefixer */
.element {
    display: flex;
    user-select: none;
}

/* 编译后 */
.element {
    display: -webkit-flex;
    display: -ms-flexbox;
    display: flex;
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
}

/* cssnext特性 */
:root {
    --primary-color: #3498db;
}

.element {
    color: var(--primary-color);
}

/* 嵌套语法 */
.card {
    & .header {
        background: blue;
    }
}
```

### 2. 常用PostCSS插件

```css
/* postcss-preset-env */
/* 现代CSS特性 */
.element {
    background: color-mod(#3498db alpha(90%));
}

/* postcss-nested */
.card {
    & .header {
        background: blue;
    }
}

/* postcss-import */
@import "components/button.css";
@import "components/card.css";

/* postcss-custom-properties */
:root {
    --theme-color: blue;
}

.element {
    color: var(--theme-color);
}
```

## 工具链配置

### 1. Sass配置

```javascript
// webpack配置
module.exports = {
    module: {
        rules: [
            {
                test: /\.scss$/,
                use: [
                    'style-loader',
                    'css-loader',
                    'sass-loader'
                ]
            }
        ]
    }
};
```

### 2. PostCSS配置

```javascript
// postcss.config.js
module.exports = {
    plugins: [
        require('autoprefixer'),
        require('postcss-preset-env'),
        require('postcss-nested'),
        require('cssnano')
    ]
};
```

## 最佳实践

### 1. 变量管理

```scss
// _variables.scss
// 颜色系统
$colors: (
    'primary': #3498db,
    'secondary': #2ecc71,
    'success': #27ae60,
    'danger': #e74c3c,
    'warning': #f1c40f,
    'info': #3498db,
    'light': #f8f9fa,
    'dark': #343a40
);

// 间距系统
$spacers: (
    0: 0,
    1: 0.25rem,
    2: 0.5rem,
    3: 1rem,
    4: 1.5rem,
    5: 3rem
);

// 断点系统
$breakpoints: (
    'xs': 0,
    'sm': 576px,
    'md': 768px,
    'lg': 992px,
    'xl': 1200px
);
```

### 2. 混合宏系统

```scss
// _mixins.scss
// 响应式设计
@mixin media-up($breakpoint) {
    $value: map-get($breakpoints, $breakpoint);
    @media (min-width: $value) {
        @content;
    }
}

// 弹性布局
@mixin flex($direction: row, $justify: flex-start, $align: stretch) {
    display: flex;
    flex-direction: $direction;
    justify-content: $justify;
    align-items: $align;
}

// 文本截断
@mixin text-truncate {
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
}
```

### 3. 模块化组织

```scss
// 文件结构
styles/
├── abstracts/
│   ├── _variables.scss
│   ├── _functions.scss
│   ├── _mixins.scss
│   └── _placeholders.scss
├── base/
│   ├── _reset.scss
│   ├── _typography.scss
│   └── _utilities.scss
├── components/
│   ├── _buttons.scss
│   ├── _cards.scss
│   └── _forms.scss
├── layout/
│   ├── _header.scss
│   ├── _footer.scss
│   └── _grid.scss
└── main.scss

// main.scss
@import 'abstracts/variables';
@import 'abstracts/functions';
@import 'abstracts/mixins';
@import 'abstracts/placeholders';

@import 'base/reset';
@import 'base/typography';
@import 'base/utilities';

@import 'components/buttons';
@import 'components/cards';
@import 'components/forms';

@import 'layout/header';
@import 'layout/footer';
@import 'layout/grid';
```

## 性能优化

### 1. 代码分割

```scss
// 按功能分割
@import 'core';      // 核心样式
@import 'components' // 组件样式
    when (media)     // 条件加载
    and (min-width: 30em);
```

### 2. 优化输出

```javascript
// PostCSS优化配置
module.exports = {
    plugins: [
        require('cssnano')({
            preset: ['default', {
                discardComments: {
                    removeAll: true,
                },
                normalizeWhitespace: false,
            }]
        })
    ]
};
```

### 3. 按需加载

```javascript
// 使用CSS Modules
.component {
    composes: base from './base.css';
    background: blue;
}

// 使用Tree Shaking
import styles from './styles.module.css';
```

## 工作流集成

### 1. 开发工具

```json
// package.json
{
    "scripts": {
        "dev": "sass --watch src/styles:dist/styles",
        "build": "sass src/styles:dist/styles --style compressed",
        "lint": "stylelint \"src/**/*.scss\"",
        "format": "prettier --write \"src/**/*.scss\""
    }
}
```

### 2. CI/CD集成

```yaml
# .gitlab-ci.yml
styles:
  script:
    - npm install
    - npm run lint
    - npm run build
  artifacts:
    paths:
      - dist/styles
```

## 总结

CSS预处理器和后处理器可以：
- 提高CSS代码的可维护性
- 增强CSS的功能
- 自动化处理前缀和优化
- 提供更好的开发体验
- 实现模块化和组件化
- 优化生产环境代码

选择合适的预处理器和后处理器，并建立良好的工作流，可以显著提高CSS开发效率。
