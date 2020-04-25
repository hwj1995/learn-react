# JSX简明入门指南

## 前言

以MVC模式来说，React主要负责View。React将所有事物看成Component，将同一个Component相关的程式与资源放在一起。撰写React Component时利用JSX提高效率

## 一、使用JSX的好处

1. ### 提供更加语意化且易懂的标识

HTML写法

```haxe
<form class="messageBox">
  <textarea></textarea>
  <button type="submit"></button>
</form>
```

JSX写法

```jsx
<MessageBox />
```

2. ### 更加简洁

不实用JSX

```jsx
<a href="https://facebook.github.io/react/">Hello!</a>
```

使用JSX

```react
// React.createElement(元件/HTML標籤, 元件屬性，以物件表示, 子元件)
React.createElement('a', {href: 'https://facebook.github.io/react/'}, 'Hello!')
```

3. ### 结合原生JavaScript语法

```react
// const 為常數
const lists = ['JavaScript', 'Java', 'Node', 'Python'];

class HelloMessage extends React.Component {
  render() {
    return (
    <ul>
      {lists.map((result, index) => {
        return (<li key={index}>{result}</li>);
      })}
    </ul>);
  }
}
```

## 二、JSX用法摘要

1. ### 环境设定与使用方法

两种使用方法

- 使用browserify或webpack等CommonJS bundler并整合到bable预处理
- 于浏览器端做解析

载入JSX方式有：

- 内嵌

```react
<script type="text/babel">
  ReactDOM.render(
    <h1>Hello, world!</h1>,
    document.getElementById('example')
  );
</script>
```

- 外部引入

```html
<script type="text/jsx" src="main.jsx"></script>
```

2. ### 标签用法

类似XML。一般Component命名首字母大写，HTML tag小写

```react
class HelloMessage extends React.Component {
  render() {
    return (
      <div>
        <p>Hello React!</p>
        <MessageList />
      </div>
    );
  }
}
```

3. ### 转换成JavaScript

解析前

```react
var text = 'Hello React';
<h1>{text}</h1>		//	变量{}
<h1>{'text'}</h1>	//	一般文字''
```

解析后

```react
var text = 'Hello React';
React.createElement("h1", null, "Hello React!");
```

4. ### 注解

```react
// 單行註解

/*
  多行註解
*/

var content = (
  <List>
      {/* 若是在子元件註解要加 {}  */}
      <Item
        /* 多行
           註解
           喔 */
        name={window.isLoggedIn ? window.name : ''} // 單行註解
      />
  </List>
);
```

5. ### 属性

JSX中使用className与htmlFor

```react
class HelloMessage extends React.Component {
  render() {
    return (
      <div className="message">
        <p>Hello React!</p>
      </div>
    );
  }
}
```

6. ### 扩展属性

```react
var props = {
  style: "width:20px",
  className: "main",
  value: "yo",  
}

<HelloMessage  {...props} value="yo" />

// 等於以下
React.createElement("h1", React._spread({}, props, {value: "yo"}), "Hello React!");
```

7. ### 自定义属性

使用data-

```react
<HelloMessage data-attr="xd" />	//	使用data-
```

8. ### 显示HTML

```react
<div>{{_html: '<h1>Hello World!!</h1>'}}</div>
```

9. ### 样式使用

通常为了信息安全，会过滤HTML，如需显示如下

```react
<HelloMessage style={{ color: '#FFFFFF', fontSize: '30px'}} />
```

10. ### 事件处理

```react
<HelloMessage onClick={this.onBtn} />
```

