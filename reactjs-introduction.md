# ReactJS与Compnent设计入门介绍

React与Component在设计时的几个主要特性

## ReactJS特性简介

重点了解一下几个特性

1. 基于元件（Component）化思考
2. 用JSX进行宣告式（Declarative）UI设计
3. 使用Virtual DOM
4. Component Prototype 防呆机制
5. Component就像状态机（State Machine），而且也有生命周期（Life Cycle）
6. 一律重绘（Always Redraw）和单向资料流（Unidirectional Data Flow）
7. 在js里写css：Inline Style

### 基于元件（Component）化思考

React最基本的单元为Component，每个Component又可以包含子元件，并且按照要求组装成组合式（Composable）元件

` <TodoApp>` 元件可以包含` <TodoHeader />`、`<TodoList />` 子元件

```react
	<div>
		<TodoHeader />
		<TodoList />
	</div>
```

`<TodoList />`又包含其他

```react
	<div>
		<ul>
			<li>寫程式碼</li>
			<li>哄妹子</li>
			<li>買書</li>
		</ul>
	</div>
```

一般React Component有两种主要撰写方式

1. 使用ES6的Class（可以進行比較複雜的操作和元件生命週期的控制，**相對於 stateless components 耗費資源**）

```react
//  注意元件開頭第一個字母都要大寫
class MyComponent extends React.Component {
	// render 是 Class based 元件唯一必須的方法（method）
	render() {
		return (
			<div>Hello, World!</div>
		);
	}
}

// 將 <MyComponent /> 元件插入 id 為 app 的 DOM 元素中
ReactDOM.render(<MyComponent/>, document.getElementById('app'));
```

2. 使用Functional Component写法（單純地 render UI 的 stateless components，沒有內部狀態、沒有實作物件和 ref，沒有生命週期函數。**若非需要控制生命週期的話建議多使用 stateless components 獲得比較好的效能**）

```javascript
// 使用 arrow function 來設計 Functional Component 讓 UI 設計更單純（f(D) => UI），減少副作用（side effect）
const MyComponent = () => (
	<div>Hello, World!</div>
);

// 將 <MyComponent /> 元件插入 id 為 app 的 DOM 元素中
ReactDOM.render(<MyComponent/>, document.getElementById('app'));
```

### 用JSX进行宣告式（Declarative）UI设计

React在设计思路上认为使用Component比起模版（Template）与显示逻辑（Display Logic）更能实现关注点分离

宣告式（Declarative）UI 設計就比單純用（Template）式的方式更易懂

```react
// 使用宣告式（Declarative）UI 設計很容易可以看出這個元件的功能
<MailForm />

// <MailForm /> 內部長相
<form>
	<input type="text" name="email" />
	<button type="submit"></button>
</form>
```

### 使用 Virtual DOM

传统Web一般使用jQuery进行DOM的直接操作，但是DOM影响Web效能==》Virtual DOM。

通过Virtual DOM的机制让App和DOM之间进行沟通。当更改DOM时，会通过React自身的diff演算算法区计算出最小更新，进而最小化更新真实的DOM

### Component Prototype 防呆机制

React提供props预设值设定（Default Prop Values），也提供Prop的验证（Validation）

```react
//  注意元件開頭第一個字母都要大寫
class MyComponent extends React.Component {
	// render 是 Class based 元件唯一必須的方法（method）
	render() {
		return (
			<div>Hello, World!</div>
		);
	}
}

// PropTypes 驗證，若傳入的 props type 不符合將會顯示錯誤
MyComponent.propTypes = {
  todo: React.PropTypes.object,
  name: React.PropTypes.string,
}

// Prop 預設值，若對應 props 沒傳入值將會使用 default 值
MyComponent.defaultProps = {
 todo: {}, 
 name: '', 
}
```

### Component就像状态机（State Machine），而且也有生命周期（Life Cycle）

根据不同的state（通过`setState()`修改）和props，Component会出现对应的显示结果

### 一律重绘（Always Redraw）和单向资料流（Unidirectional Data Flow）

props无法修改，state通过setState()修改。当props或state更新时，重绘整个UI。而 React 透過整合 Flux 或 Flux-like（例如：Redux）可以更具體實現單向資料流（Unidirectional Data Flow），讓資料流的管理更為清晰

### 在js里写css：Inline Style

```react
const divStyle = {
  color: 'red',
  backgroundImage: 'url(' + imgUrl + ')',
};

ReactDOM.render(<div style={divStyle}>Hello World!</div>, document.getElementById('app'));
```

