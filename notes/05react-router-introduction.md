# React Router 入门实战教学

## 前言

进行比较复杂的应用程式开发并介绍不刷页应用程式（singel page application）

## 单页式应用程式

- 传统的Web开发主要由服务器管理URL Routing和渲染HTML页面，每次URL一换就需要重新载入页面
- 单页式应用程式，由前端负责URL的routing管理，若需要和后端进行API资料沟通的话，通常使用Ajax

## 开始React Routing

HTML 

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>ReactRouter</title>
  <link rel="stylesheet" type="text/css" href="../res/styles/main.css">
</head>
<body>
	<div id="app"></div>
</body>
</html>
```

index.js

```react
import React from 'react';
import ReactDOM from 'react-dom';
import { Router, Route, hashHistory, IndexRoute } from 'react-router';
import App from './components/App';
import Home from './components/Home';
import Repos from './components/Repos';
import About from './components/About';
import User from './components/User';
import Contacts from './components/Contacts';

ReactDOM.render(
  <Router history={hashHistory}>			//	Router本身不定义routing
    <Route path="/" component={App}>	//	负责URL和对应的元件的关系，可以嵌套
      <IndexRoute component={Home} />	//	对于URL为/的情况
      <Route path="/repos/:name" component={Repos} />
      <Route path="/about" component={About} />
      <Route path="/user" component={User} />
      <Route path="/contacts" component={Contacts} />
    </Route>
  </Router>,
  document.getElementById('app'));

  /* 另外一種寫法：
	const routes = (
	    <Route path="/" component={App}>
	      <IndexRoute component={Home} />
	      <Route path="/repos/:name" component={Repos} />
	      <Route path="/about" component={About} />
	      <Route path="/user" component={User} />
	      <Route path="/contacts" component={Contacts} />
	    </Route>
	);

	ReactDOM.render(
	  <Router routes={routes} history={hashHistory} />,
	  document.getElementById('app'));
  */
```

src/components/App/App.js

```react
import React from 'react';
import { Link, IndexLink } from 'react-router';
import styles from './appStyles';
import NavLink from '../NavLink';

const App = (props) => (
  <div>
    <h1>React Router Tutorial</h1>
    <ul>
      <li><IndexLink to="/" activeClassName="active">Home</IndexLink></li>
      <li><Link to="/about" activeStyle={{ color: 'green' }}>About</Link></li>
      <li><Link to="/repos/react-router" activeStyle={styles.active}>Repos</Link></li>
      <li><Link to="/user" activeClassName="active">User</Link></li>
      <li><NavLink to="/contacts">Contacts</NavLink></li>
    </ul>
    <!-- 我們將 App 元件當做每個元件都會載入的母模版，因此可以透過 children 載入對應 URL 的子元件 -->
    {props.children}
  </div>
);

App.propTypes = {
  children: React.PropTypes.object,
};

export default App;
```

