## 响应事件
### 添加事件处理函数
```js
export default function Button() {
  function handleClick() {
    alert('你点击了我！');
  }

  return (
    <button onClick={handleClick}>
      点我
    </button>
  );
}
```
```js
// 内联的事件处理函数
<button onClick={function handleClick() {
  alert('你点击了我！');
}}>
// 箭头函数
<button onClick={() => {
  alert('你点击了我！');
}}>
  点我
</button>
```

## 在事件处理函数中读取props
```js
function AlertButton({ message, children }) {
  return (
    <button onClick={() => alert(message)}>
      {children}
    </button>
  );
}

export default function Toolbar() {
  return (
    <div>
      <AlertButton message="正在播放！">
        播放电影
      </AlertButton>
      <AlertButton message="正在上传！">
        上传图片
      </AlertButton>
    </div>
  );
}
```
## 将事件处理函数作为props传递
```js
function AlertButton({ message, children }) {
  return (
    <button onClick={() => alert(message)}>
      {children}
    </button>
  );
}
function PlayButton({ movieName }) {
  function handlePlayClick() {
    alert(`正在播放 ${movieName}！`);
  }

  return (
    <Button onClick={handlePlayClick}>
      播放 "{movieName}"
    </Button>
  );
}

function UploadButton() {
  return (
    <Button onClick={() => alert('正在上传！')}>
      上传图片
    </Button>
  );
}

export default function Toolbar() {
  return (
    <div>
      <PlayButton movieName="魔女宅急便" />
      <UploadButton />
    </div>
  );
}
```
## 命名事件处理函数 prop
Button 组件的 onClick prop 本来也可以被命名为 onSmash：
```js
function Button({ onSmash, children }) {
  return (
    <button onClick={onSmash}>
      {children}
    </button>
  );
}

export default function App() {
  return (
    <div>
      <Button onSmash={() => alert('正在播放！')}>
        播放电影
      </Button>
      <Button onSmash={() => alert('正在上传！')}>
        上传图片
      </Button>
    </div>
  );
}
```     

## 事件传播

点击任一按钮，它自身的 onClick 将首先执行，然后父级 <div> 的 onClick 会接着执行。因此会出现两条消息。如果你点击 toolbar 本身，将只有父级 <div> 的 onClick 会执行。



```js
export default function Toolbar() {
  return (
    <div className="Toolbar" onClick={() => {
      alert('你点击了 toolbar ！');
    }}>
      <button onClick={() => alert('正在播放！')}>
        播放电影
      </button>
      <button onClick={() => alert('正在上传！')}>
        上传图片
      </button>
    </div>
  );
}
```


## 阻止传播

```js
function Button({ onClick, children }) {
  return (
    <button onClick={e => {
      e.stopPropagation();
      onClick();
    }}>
      {children}
    </button>
  );
}

export default function Toolbar() {
  return (
    <div className="Toolbar" onClick={() => {
      alert('你点击了 toolbar ！');
    }}>
      <Button onClick={() => alert('正在播放！')}>
        播放电影
      </Button>
      <Button onClick={() => alert('正在上传！')}>
        上传图片
      </Button>
    </div>
  );
}
```
## 传递处理函数作为事件传播的替代方案

```js
function Button({ onClick, children }) {
  return (
    <button onClick={e => {
      e.stopPropagation();
      onClick();
    }}>
      {children}
    </button>
  );
}
```

## 阻止默认行为 

某些浏览器事件具有与事件相关联的默认行为。例如，点击 <form> 表单内部的按钮会触发表单提交事件，默认情况下将重新加载整个页面：

```js
export default function Signup() {
  return (
    <form onSubmit={() => alert('提交表单！')}>
      <input />
      <button>发送</button>
    </form>
  );
}
```
可以调用事件对象中的 e.preventDefault() 来阻止这种情况发生
```js
export default function Signup() {
  return (
    <form onSubmit={e => {
      e.preventDefault();
      alert('提交表单！');
    }}>
      <input />
      <button>发送</button>
    </form>
  );
}

```
<ul>e.stopPropagation() 阻止触发绑定在外层标签上的事件处理函数。</ul>
<ul>e.preventDefault() 阻止少数事件的默认浏览器行为。</ul>
<ul>你可以通过将函数作为 prop 传递给元素如 <button> 来处理事件。
必须传递事件处理函数，而非函数调用！ onClick={handleClick} ，不是 onClick={handleClick()}。
你可以单独或者内联定义事件处理函数。
事件处理函数在组件内部定义，所以它们可以访问 props。
你可以在父组件中定义一个事件处理函数，并将其作为 prop 传递给子组件。
你可以根据特定于应用程序的名称定义事件处理函数的 prop。
事件会向上传播。通过事件的第一个参数调用 e.stopPropagation() 来防止这种情况。
事件可能具有不需要的浏览器默认行为。调用 e.preventDefault() 来阻止这种情况。
从子组件显式调用事件处理函数 prop 是事件传播的另一种优秀替代方案。</ul>









