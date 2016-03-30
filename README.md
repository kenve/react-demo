##React是什么
1. facebook 2013 发布
2. React 兼容IE8+

## Html Template
React官网提供的Html模板，所有demo都是在这个Html模板内编写的
```html
<!DOCTYPE html>
<html>

<head>
    <meta charset="UTF-8" />
    <title>Hello React!</title>
    <script src="../build/react.js"></script>
    <script src="../build/react-dom.js"></script>
    <script src="../build/browser.min.js"></script>
</head>

<body>
    <div id="example"></div>
    <script type="text/babel">
        // ** Our code goes here! **
        // 在这里书写jsx代码
    </script>
</body>
</html>
```
上面的html模板有几个地方要注意：
 * 要在`head`便签中引入`react.js`、`react-dom.js`、`browser.min.js`三个js库,而且要在jsx代码前引入，其中，`react.js` 是 React 的核心库，`react-dom.js` 是提供与 DOM 相关的功能，`Browser.js` 的作用是将 JSX 语法转为 JavaScript语法，这一步很消耗时间，实际上线的时候，应该使用构建工具构建完成后在放到服务器中。
 * 因为 React 独有的 JSX 语法，跟 JavaScript 不兼容。凡是使用 JSX 的地方，都要加上 `type="text/babel"`,所以`body`中的 `<script>` 标签的 `type` 属性为 `text/babel`。

## HelloWord 
官网提供了一个非常简单的HelloWord 的代码，将如下嵌入html模板中即可:
```javascript
<script type="text/babel">
      ReactDOM.render(
        <h1>Hello, world!</h1>,
        document.getElementById('example')
      );
    </script>
```
上面代码是将一个`h1`便签，插入`id`为`example`的dom节点下（查看代码 [helloword](http://facebook.github.io/react/docs/displaying-data.html#jsx-syntax) ）
## JSX
#### 什么是JSX
   * JSX=JavaScript XML
   * 是基于ECMAScript的一种新特性
   * 一种定义带属性结构的语法
   * JSX不是XML或者HTML,而是一种机制

#### JSX的特点
   * 类XML语法容易接受
   * 结构清晰
   * 增强js语义
   * 抽象程度高（跨平台）
   * 代码模块化
   * 从左到右

#### JSX的语法:
   jsx代码要使用`<script type="text/babel"></script>`标签包裹,JSX 的基本语法规则：遇到 HTML 标签（以 `<` 开头），就用 HTML 规则解析；遇到代码块（以 `{` 开头），就用 JavaScript 规则解析。所以允许 HTML 与 JavaScript 的混写。

```javascript
      //调用ReactDOM的render方法，把组件渲染到页面中
      //render接收两个参数，第一个是：一段jsx代码，第二个是渲染目标
      ReactDOM.render(
        <h1>Hello, world!</h1>,
        document.getElementById('example')
      );
```

   以上代码定义了一个名为`HelloWord`的组件，然后调用`ReactDOM.render();`方法;该方法需要传递两个参数，第一个参数是一段JSX代码,第二参数是要渲染目标节点。
#### jsx组件
   React 允许将代码封装成组件（component），然后像插入普通 HTML 标签一样，在网页中插入这个组件。`React.createClass` 方法就用于生成一个组件类。(查看代码[jsx-component](jsx/jsx-component.html))。

```javascript
     //创建名为HelloWord的组件
    var HelloWorld = React.createClass({
        render: function() {
            return ( < p >
                Hello, < input type = "text"
                placeholder = "Your name here" / > !It is { this.props.date.toTimeString() } < /p>
            );
        }
    });
  setInterval(function() {
      //调用React的render方法，把组件渲染到页面中
      //前面声明组件可以当作标签来使用，即<HelloWorld />
      //将名称为的属性date值，传入自定义组件中
      ReactDOM.render( < HelloWorld date = { new Date() }/>, document.getElementById('example') ); 
    }, 500);
```

* 上面代码中，变量 `HelloWord` 就是一个组件类,模板插入 `<HelloWord />` 时，会自动生成 `HelloMessage` 的一个实例（下文的"组件"都指组件类的实例）。所有组件类都必须有自己的 `render` 方法，用于输出组件。
* 注意，组件类的首字母必须大写,使用驼峰命名法，否则会报错。另外，组件类只能包含一个顶层标签，否则也会报错。组件类可以任意加入属性像加HTML的属性一样，比如：`< HelloWorld date = { new Date() }/>` 就是在`HelloWord`组件中加入属性`date`，值为`new Date()`,因为是求值表达式所以要用`{}`包裹，也可以直接`<HelloWord name="Tom">`。
* 组件的属性可以在组件类的 this.props 对象上获取，比如 `date` 属性就可以通过 `this.props.data` 读取。
* 添加组件属性，有一个地方需要注意，就是 `class` 属性需要写成 `className` ，`for` 属性需要写成 `htmlFor` ，这是因为 `class` 和 `for` 是 JavaScript 的保留字。

#### JSX注释
多行注释使用`/**/`,单行注释使用 `//`
```js
 var HelloWorld = React.createClass({
        render: function () {
          return (
	          <p
	            /*
	            comment...
	            */
	            name="test" // set name to test
	          >Hello, World {
	            /*
	            comment...
	            comment
	            */

	            "hello, "

	            // comment...
	          }</p>
          )
        }
      });
```
#### JSX的设置CSS样式

```js
var style={
    color:'red',
    border:'1px solid #000'
 };
var HelloWorld = React.createClass({
    render: function() {
        return ( 
          <div style={style}>
          < p >
            Hello, World < /p>
          </div>
        );
    }
});
ReactDOM.render( < HelloWorld/>, document.getElementById('example') ); 
```
#### 条件判断语句
{}不能直接写条件判断（ifelse）
 * 使用三元表达式进行条件判断(查看[Demo](jsx/jsx-judgment01.html))

```js
var HelloWorld = React.createClass({
    render: function() {
        return ( 
          <div>
          < p >
            Hello, {this.props.name?this.props.name:'World'} < /p>
          </div>
        );
    }
});
ReactDOM.render( < HelloWorld/>, document.getElementById('example') ); 
```
 * 使用自定义函数返回值，接受返回值进行条件判断(查看[demo](jsx/jsx-judgment02.html))

```js
var HelloWorld = React.createClass({			
	getName:function () {
	    if (this.props.name) {
	        return this.props.name;
	    } else {
	        return 'World';
	    }
	},
	render: function() {
	    var name=this.getName();
	    return ( 
	      <div>
	      < p >
	        Hello, {name} < /p>
	      </div>
	    );
	}
	});
ReactDOM.render( < HelloWorld/>, document.getElementById('example') ); 
```
 * 直接调用自定义函数进行条件判断(查看[demo](jsx/jsx-judgment03.html))

```js
var HelloWorld = React.createClass({			
	getName:function () {
	    if (this.props.name) {
	        return this.props.name;
	    } else {
	        return 'World';
	    }
	},
	render: function() {
	    return ( 
	      <div>
	      < p >
	        Hello, { this.getName()} < /p>
	      </div>
	    );
	}
	});
ReactDOM.render( < HelloWorld/>, document.getElementById('example') ); 
```
 * 使用比较运算符，代替条件判断(查看[demo](jsx/jsx-judgment04.html))。
```js
 var HelloWorld = React.createClass({
    render: function() {
        return ( 
          <div>
          < p >
            Hello, {this.props.name || 'World'} < /p>
          </div>
        );
    }
});
ReactDOM.render( < HelloWorld/>, document.getElementById('example') ); 
```
* 使用万能的函数表达式 （一般不这样写）：
```js
 var HelloWorld = React.createClass({
    render: function() {
        return ( 
          <div>
          < p >
            Hello, {(function (obj) {
                if (obj.props.name) {
                    return obj.props.name;
                } else {
                    return 'World';
                }
            })(this)} < /p>
          </div>
        );
    }
});
ReactDOM.render( < HelloWorld/>, document.getElementById('example') );
```
#### 非dom 属性
非DOM属性：dangerouslySetInnerHTML、ref、key
节点相似尽量写成一个，因为react会重新生成； 使用列表展示元素，元素加上key
![React Diff算法流程](images/diff.png)

 * dangerouslySetInnerHTML：在JSX中直接插入HTML代码

```js
var rawHTML={
    __html:"<h1>I'm inner HTML</h1>"
}
var HelloWorld = React.createClass({

    render: function() {
        return ( 
          <div dangerouslySetInnerHTML={rawHTML}>
          </div>
        );
    }
});
ReactDOM.render( < HelloWorld/>, document.getElementById('example') );
```
 * ref:父组件引用子组件

```js
var HelloWorld = React.createClass({
    render: function() {
        return ( 
          <div>
          <p ref="childp">
               "Hello, World"
          </p>
          </div>
        );
    }
});
ReactDOM.render( < HelloWorld/>, document.getElementById('example') ); 
```
 * key：提高渲染性能,不能出现相同的key,key值必须是唯一的

```js
var HelloWorld = React.createClass({
    render: function() {
        return ( 
          <ul>
            <li key="1">1</li>
            <li key="2">2</li>
            <li key="3">3</li>
        </ul>
        );
    }
});
ReactDOM.render( < HelloWorld/>, document.getElementById('example') ); 
```
#### JSX源码
## React组件生命周期详解
#### 什么是组件的生命周期
 * 组件本质上是状态机，输入确定，输出一定确定。
 * 状态发生转换时会触发不同的钩子函数，从而让开发者有机会做出响应。
 * 可以用事件的思路来理解状态。
 * 不同生命周期内可以自定义的函数。
 * 组件生命周期可以分为：初始化 → 运行中 → 销毁，即：Mounting（已插入真实`DOM`）→ Updating(正在被重新渲染) → Unmounting(已移出真实`DOM`)

#### 初始化阶段函数介绍
初始化阶段可以使用的函数：
 * getDefaultProps：只调用一次，实例之间共享引用
 * getInitialState：初始化每个实例特有的状态
 * componentWillMount：render之前最后一次修改状态的机会
 * render：只能访问this.props和this.state，只有一个顶层组件，不允许修改状态和DOM输出。
 * componentDidMount：成功render并渲染完成真实DOM之后触发，可以修改DOM

使用实例：
 * 触发顺序`getDefaultProps` → `getInitialState` → `componentWillMount` → `render` → `componentDidMount`
```js
var HelloWorld = React.createClass({ 
    	//只调用一次，实例之间共享引用
     	getDefaultProps:function () {
     		console.log('getDefaultProps,1');
     	},
     	//初始化每个实例特有的状态
     	getInitialState:function () {
     		console.log('getInitialState,2');
     		return null;
     	},
     	//render之前最后一次修改状态的机会
     	componentWillMount:function () {
     		console.log('componentWillMount,3');
     	},
     	//只能访问this.props和this.state，只有一个顶层组件，不允许修改状态和DOM输出
     	render: function() { 
     		console.log('render,4');
         	return (
		       <div>
		           <p>
		             Hello, World！
		            </p>
		       </div>
     	    ); 
       },
       //成功render并渲染完成真实DOM之后触发，可以修改DOM
        componentDidMount:function () {
        	console.log('componentDidMount,5');
        }
   }); 
ReactDOM.render(<HelloWorld/>, document.getElementById('example') );
```
 * 用法

```js
var count=0;
var HelloWorld = React.createClass({ 
	//只调用一次，实例之间共享引用
 	getDefaultProps:function () {
 		console.log('getDefaultProps,1');
 		return {name:'Tom'};
 	},
 	//初始化每个实例特有的状态
 	getInitialState:function () {
 		console.log('getInitialState,2');
 		return {
 			myCount:count++,
 			ready:false
 		};
 	},
 	//render之前最后一次修改状态的机会
 	componentWillMount:function () {
 		console.log('componentWillMount,3');
 		this.setState({
 			ready:true
 		})
 	},
 	//只能访问this.props和this.state，只有一个顶层组件，不允许修改状态和DOM输出
 	render: function() { 
 		console.log('render,4');
     	return (
	           <p>
	             Hello, {this.props.name ? this.props.name : "World"}<br/>{"ready:" + this.state.ready} <br/>{"count:"+this.state.myCount}
	            </p>
 	    ); 
   },
   //成功render并渲染完成真实DOM之后触发，可以修改DOM
    componentDidMount:function () {
    	console.log('componentDidMount,5');
    	$(ReactDOM.findDOMNode(this)).append('surprise!');
    }
}); 
ReactDOM.render(<div><HelloWorld/><br/><HelloWorld/></div>, document.getElementById('example') );
```
输出的页面及控制台信息如下：
![页面显示结果](mounting02-result.png) ![控制台信息](images/mounting02-console-result.png)

#### 运行中阶段函数介绍


