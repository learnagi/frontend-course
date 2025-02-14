---
title: "JavaScript事件"
slug: "javascript-events"
sequence: 15
description: "详细介绍JavaScript事件的使用方法和事件处理"
is_published: true
estimated_minutes: 30
language: "zh-CN"
---

# JavaScript事件

## 事件基础

### 1. 事件类型

```javascript
// 常见DOM事件
// 鼠标事件
element.onclick = function() {};       // 点击
element.ondblclick = function() {};    // 双击
element.onmouseover = function() {};   // 鼠标移入
element.onmouseout = function() {};    // 鼠标移出

// 键盘事件
element.onkeydown = function() {};     // 键盘按下
element.onkeyup = function() {};       // 键盘释放
element.onkeypress = function() {};    // 键盘按压

// 表单事件
element.onsubmit = function() {};      // 表单提交
element.onreset = function() {};       // 表单重置
element.onchange = function() {};      // 值改变
element.onfocus = function() {};       // 获得焦点
element.onblur = function() {};        // 失去焦点

// 文档/窗口事件
window.onload = function() {};         // 加载完成
window.onresize = function() {};       // 调整大小
window.onscroll = function() {};       // 滚动
```

### 2. 事件注册

```javascript
// 方法一：HTML属性
<button onclick="handleClick()">点击</button>

// 方法二：DOM属性
const button = document.querySelector('button');
button.onclick = function() {
    console.log('按钮被点击');
};

// 方法三：addEventListener
button.addEventListener('click', function() {
    console.log('按钮被点击');
});

// 移除事件监听器
function handleClick() {
    console.log('按钮被点击');
}
button.addEventListener('click', handleClick);
button.removeEventListener('click', handleClick);
```

## 事件对象

### 1. 事件属性

```javascript
// 事件对象的常用属性
element.addEventListener('click', function(event) {
    console.log(event.type);      // 事件类型
    console.log(event.target);    // 触发事件的元素
    console.log(event.currentTarget); // 当前处理事件的元素
    console.log(event.timeStamp); // 事件发生的时间戳
});

// 鼠标事件属性
element.addEventListener('mousemove', function(event) {
    console.log(event.clientX);   // 鼠标X坐标（相对视口）
    console.log(event.clientY);   // 鼠标Y坐标（相对视口）
    console.log(event.pageX);     // 鼠标X坐标（相对文档）
    console.log(event.pageY);     // 鼠标Y坐标（相对文档）
    console.log(event.button);    // 按下的鼠标按钮
});

// 键盘事件属性
element.addEventListener('keydown', function(event) {
    console.log(event.key);       // 按键值
    console.log(event.keyCode);   // 按键代码
    console.log(event.ctrlKey);   // Ctrl键是否按下
    console.log(event.shiftKey);  // Shift键是否按下
    console.log(event.altKey);    // Alt键是否按下
});
```

### 2. 事件方法

```javascript
// 阻止默认行为
form.addEventListener('submit', function(event) {
    event.preventDefault();  // 阻止表单提交
});

// 阻止事件冒泡
child.addEventListener('click', function(event) {
    event.stopPropagation();  // 阻止事件向上冒泡
});

// 立即阻止事件冒泡
child.addEventListener('click', function(event) {
    event.stopImmediatePropagation();  // 阻止其他事件处理程序
});
```

## 事件流

### 1. 事件冒泡和捕获

```javascript
// 事件冒泡（默认）
element.addEventListener('click', function(event) {
    console.log('冒泡阶段');
}, false);

// 事件捕获
element.addEventListener('click', function(event) {
    console.log('捕获阶段');
}, true);

// 事件委托
document.getElementById('parent').addEventListener('click', function(event) {
    if (event.target.matches('.child')) {
        console.log('子元素被点击');
    }
});
```

### 2. 自定义事件

```javascript
// 创建自定义事件
const customEvent = new CustomEvent('myEvent', {
    detail: {
        message: '这是自定义事件'
    },
    bubbles: true,
    cancelable: true
});

// 触发自定义事件
element.dispatchEvent(customEvent);

// 监听自定义事件
element.addEventListener('myEvent', function(event) {
    console.log(event.detail.message);
});
```

## 事件处理

### 1. 事件处理函数

```javascript
// 普通事件处理函数
function handleClick(event) {
    console.log('按钮被点击');
}

// 箭头函数处理事件
const handleMouseOver = (event) => {
    console.log('鼠标移入');
};

// 事件处理对象
const handlers = {
    handleClick(event) {
        console.log('点击事件');
    },
    handleMouseOver(event) {
        console.log('移入事件');
    }
};
```

### 2. 事件委托模式

```javascript
// 事件委托实现
function delegate(parent, selector, eventType, handler) {
    parent.addEventListener(eventType, function(event) {
        const targetElement = event.target.closest(selector);
        
        if (targetElement && parent.contains(targetElement)) {
            handler.call(targetElement, event);
        }
    });
}

// 使用示例
delegate(document.getElementById('list'), 'li', 'click', function(event) {
    console.log('列表项被点击:', this.textContent);
});
```

## 常见事件应用

### 1. 表单验证

```javascript
// 表单验证示例
const form = document.getElementById('myForm');
const emailInput = document.getElementById('email');

emailInput.addEventListener('input', function(event) {
    const email = event.target.value;
    const isValid = /\S+@\S+\.\S+/.test(email);
    
    if (!isValid) {
        emailInput.setCustomValidity('请输入有效的邮箱地址');
    } else {
        emailInput.setCustomValidity('');
    }
});

form.addEventListener('submit', function(event) {
    if (!form.checkValidity()) {
        event.preventDefault();
        // 显示错误信息
    }
});
```

### 2. 拖拽功能

```javascript
// 拖拽功能实现
function enableDrag(element) {
    let isDragging = false;
    let currentX;
    let currentY;
    let initialX;
    let initialY;
    
    element.addEventListener('mousedown', dragStart);
    document.addEventListener('mousemove', drag);
    document.addEventListener('mouseup', dragEnd);
    
    function dragStart(event) {
        initialX = event.clientX - currentX;
        initialY = event.clientY - currentY;
        
        if (event.target === element) {
            isDragging = true;
        }
    }
    
    function drag(event) {
        if (isDragging) {
            event.preventDefault();
            currentX = event.clientX - initialX;
            currentY = event.clientY - initialY;
            
            element.style.transform = 
                `translate(${currentX}px, ${currentY}px)`;
        }
    }
    
    function dragEnd(event) {
        initialX = currentX;
        initialY = currentY;
        isDragging = false;
    }
}
```

## 性能优化

### 1. 事件节流

```javascript
// 节流函数
function throttle(func, limit) {
    let inThrottle;
    return function(...args) {
        if (!inThrottle) {
            func.apply(this, args);
            inThrottle = true;
            setTimeout(() => inThrottle = false, limit);
        }
    };
}

// 使用示例
const throttledScroll = throttle(function() {
    console.log('滚动事件');
}, 1000);

window.addEventListener('scroll', throttledScroll);
```

### 2. 事件防抖

```javascript
// 防抖函数
function debounce(func, delay) {
    let timeoutId;
    return function(...args) {
        clearTimeout(timeoutId);
        timeoutId = setTimeout(() => {
            func.apply(this, args);
        }, delay);
    };
}

// 使用示例
const debouncedResize = debounce(function() {
    console.log('窗口大小改变');
}, 500);

window.addEventListener('resize', debouncedResize);
```

## 实践示例

### 1. 图片懒加载

```javascript
// 图片懒加载实现
function lazyLoad() {
    const images = document.querySelectorAll('img[data-src]');
    const imageObserver = new IntersectionObserver((entries, observer) => {
        entries.forEach(entry => {
            if (entry.isIntersecting) {
                const img = entry.target;
                img.src = img.dataset.src;
                img.removeAttribute('data-src');
                observer.unobserve(img);
            }
        });
    });
    
    images.forEach(img => imageObserver.observe(img));
}

// 使用示例
document.addEventListener('DOMContentLoaded', lazyLoad);
```

### 2. 无限滚动

```javascript
// 无限滚动实现
function infiniteScroll(callback, options = {}) {
    const {
        root = null,
        rootMargin = '0px',
        threshold = 0.1
    } = options;
    
    const observer = new IntersectionObserver(
        (entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    callback();
                }
            });
        },
        { root, rootMargin, threshold }
    );
    
    // 观察目标元素
    const target = document.querySelector('#sentinel');
    observer.observe(target);
}

// 使用示例
infiniteScroll(() => {
    // 加载更多内容
    loadMoreContent();
});
```

## 最佳实践

1. 事件绑定
   ```javascript
   // 推荐：使用addEventListener
   element.addEventListener('click', handleClick);
   
   // 不推荐：直接赋值
   // element.onclick = handleClick;
   ```

2. 事件委托
   ```javascript
   // 推荐：使用事件委托
   document.getElementById('list').addEventListener('click', function(event) {
       if (event.target.matches('li')) {
           // 处理列表项点击
       }
   });
   
   // 不推荐：为每个子元素绑定事件
   // document.querySelectorAll('li').forEach(item => {
   //     item.addEventListener('click', handleClick);
   // });
   ```

3. 性能考虑
   ```javascript
   // 使用节流和防抖
   const optimizedScroll = throttle(function() {
       // 滚动处理逻辑
   }, 100);
   
   const optimizedResize = debounce(function() {
       // 调整大小处理逻辑
   }, 250);
   ```

## 总结

- 掌握事件基础知识
- 理解事件对象属性
- 使用事件流机制
- 实现事件处理模式
- 优化事件性能
- 遵循最佳实践

下一章将介绍JavaScript字符串。
