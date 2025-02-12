---
title: "CSS变换与动画"
slug: "css-transforms-animations"
sequence: 12
description: "掌握CSS变换和动画效果的创建方法"
is_published: true
estimated_minutes: 40
language: "zh-CN"
---

# CSS变换与动画

## 变换（Transform）

### 1. 2D变换

```css
.transform-2d {
    /* 平移 */
    transform: translate(50px, 100px);
    transform: translateX(50px);
    transform: translateY(100px);
    
    /* 缩放 */
    transform: scale(2);
    transform: scale(2, 1.5);
    transform: scaleX(2);
    transform: scaleY(1.5);
    
    /* 旋转 */
    transform: rotate(45deg);
    
    /* 倾斜 */
    transform: skew(10deg, 20deg);
    transform: skewX(10deg);
    transform: skewY(20deg);
}
```

### 2. 3D变换

```css
.transform-3d {
    /* 开启3D空间 */
    transform-style: preserve-3d;
    perspective: 1000px;
    
    /* 3D平移 */
    transform: translate3d(x, y, z);
    transform: translateZ(100px);
    
    /* 3D旋转 */
    transform: rotate3d(1, 1, 1, 45deg);
    transform: rotateX(45deg);
    transform: rotateY(45deg);
    transform: rotateZ(45deg);
    
    /* 3D缩放 */
    transform: scale3d(2, 2, 2);
    transform: scaleZ(2);
}
```

### 3. 多重变换

```css
.multiple-transforms {
    /* 组合多个变换 */
    transform: translate(100px, 100px) rotate(45deg) scale(1.5);
    
    /* 变换原点 */
    transform-origin: center center;
    transform-origin: top left;
    transform-origin: 50% 50%;
}
```

## 过渡（Transition）

### 1. 基本过渡

```css
.transition-basic {
    /* 单个属性过渡 */
    transition: opacity 0.3s ease;
    
    /* 多个属性过渡 */
    transition: 
        opacity 0.3s ease,
        transform 0.5s ease-out;
        
    /* 所有属性过渡 */
    transition: all 0.3s ease;
}
```

### 2. 过渡属性

```css
.transition-properties {
    /* 详细配置 */
    transition-property: transform;
    transition-duration: 0.3s;
    transition-timing-function: ease;
    transition-delay: 0.1s;
    
    /* 自定义贝塞尔曲线 */
    transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
    
    /* 阶跃函数 */
    transition-timing-function: steps(4, end);
}
```

### 3. 常见过渡效果

```css
/* 悬停效果 */
.hover-effect {
    transition: all 0.3s ease;
}

.hover-effect:hover {
    transform: scale(1.1);
    box-shadow: 0 5px 15px rgba(0,0,0,0.3);
}

/* 点击效果 */
.click-effect {
    transition: transform 0.1s ease;
}

.click-effect:active {
    transform: scale(0.95);
}
```

## 动画（Animation）

### 1. 关键帧定义

```css
/* 定义关键帧 */
@keyframes slide-in {
    0% {
        transform: translateX(-100%);
        opacity: 0;
    }
    100% {
        transform: translateX(0);
        opacity: 1;
    }
}

@keyframes pulse {
    0%, 100% {
        transform: scale(1);
    }
    50% {
        transform: scale(1.1);
    }
}
```

### 2. 应用动画

```css
.animated-element {
    /* 基本动画 */
    animation: slide-in 1s ease-out;
    
    /* 详细配置 */
    animation-name: slide-in;
    animation-duration: 1s;
    animation-timing-function: ease-out;
    animation-delay: 0.5s;
    animation-iteration-count: infinite;
    animation-direction: alternate;
    animation-fill-mode: forwards;
    animation-play-state: running;
}
```

### 3. 多重动画

```css
.multiple-animations {
    /* 同时应用多个动画 */
    animation: 
        slide-in 1s ease-out,
        fade-in 2s ease-in;
}
```

## 高级动画技巧

### 1. 性能优化

```css
.optimized-animation {
    /* 使用transform和opacity进行动画 */
    transform: translateZ(0);  /* 启用GPU加速 */
    will-change: transform, opacity;
    
    /* 避免使用耗性能的属性 */
    animation: slide 0.3s ease;
}

@keyframes slide {
    from {
        transform: translateX(0);
    }
    to {
        transform: translateX(100px);
    }
}
```

### 2. 动画状态控制

```css
.controllable-animation {
    animation: bounce 1s infinite;
}

/* 暂停动画 */
.controllable-animation.paused {
    animation-play-state: paused;
}

/* 反向播放 */
.controllable-animation.reverse {
    animation-direction: reverse;
}
```

### 3. 响应式动画

```css
@media (prefers-reduced-motion: reduce) {
    .motion-safe {
        animation: none;
        transition: none;
    }
}

@media (min-width: 768px) {
    .responsive-animation {
        animation-duration: 0.5s;
    }
}
```

## 实用动画示例

### 1. 加载动画

```css
/* 旋转加载器 */
.spinner {
    width: 40px;
    height: 40px;
    border: 4px solid #f3f3f3;
    border-top: 4px solid #3498db;
    border-radius: 50%;
    animation: spin 1s linear infinite;
}

@keyframes spin {
    0% { transform: rotate(0deg); }
    100% { transform: rotate(360deg); }
}

/* 脉冲加载器 */
.pulse {
    width: 20px;
    height: 20px;
    background: #3498db;
    border-radius: 50%;
    animation: pulse 1.5s ease infinite;
}

@keyframes pulse {
    0% { transform: scale(0.8); opacity: 0.5; }
    50% { transform: scale(1.2); opacity: 1; }
    100% { transform: scale(0.8); opacity: 0.5; }
}
```

### 2. 交互动画

```css
/* 按钮悬停效果 */
.button {
    padding: 10px 20px;
    background: #3498db;
    color: white;
    border: none;
    border-radius: 4px;
    transition: all 0.3s ease;
}

.button:hover {
    transform: translateY(-2px);
    box-shadow: 0 5px 15px rgba(0,0,0,0.2);
}

/* 卡片翻转效果 */
.card {
    position: relative;
    width: 200px;
    height: 300px;
    transform-style: preserve-3d;
    transition: transform 0.6s;
}

.card:hover {
    transform: rotateY(180deg);
}

.card-front,
.card-back {
    position: absolute;
    width: 100%;
    height: 100%;
    backface-visibility: hidden;
}

.card-back {
    transform: rotateY(180deg);
}
```

### 3. 页面过渡

```css
/* 页面进入动画 */
.page-enter {
    animation: fadeIn 0.5s ease-out;
}

@keyframes fadeIn {
    from {
        opacity: 0;
        transform: translateY(20px);
    }
    to {
        opacity: 1;
        transform: translateY(0);
    }
}

/* 模态框动画 */
.modal {
    opacity: 0;
    transform: scale(0.9);
    transition: all 0.3s ease-in-out;
}

.modal.active {
    opacity: 1;
    transform: scale(1);
}
```

## 最佳实践

### 1. 性能考虑

```css
/* 使用高性能属性 */
.performant {
    transform: translate3d(0, 0, 0);  /* 启用GPU加速 */
    backface-visibility: hidden;
    perspective: 1000px;
}

/* 避免过度动画 */
@media (prefers-reduced-motion: reduce) {
    * {
        animation-duration: 0.01ms !important;
        animation-iteration-count: 1 !important;
        transition-duration: 0.01ms !important;
        scroll-behavior: auto !important;
    }
}
```

### 2. 可访问性

```css
/* 提供无动画选项 */
.accessible-animation {
    animation: bounce 1s infinite;
}

@media (prefers-reduced-motion: reduce) {
    .accessible-animation {
        animation: none;
    }
}
```

### 3. 维护性

```css
:root {
    --animation-speed: 0.3s;
    --animation-easing: ease-in-out;
}

.maintainable {
    transition: all var(--animation-speed) var(--animation-easing);
}

/* 使用有意义的动画名称 */
@keyframes slide-from-left {
    /* ... */
}
```

## 总结

掌握CSS变换和动画可以：
- 创建流畅的用户界面过渡
- 提供有意义的交互反馈
- 增强用户体验
- 创建引人注目的视觉效果

记住要平衡动画效果和性能，确保动画增强而不是干扰用户体验。
