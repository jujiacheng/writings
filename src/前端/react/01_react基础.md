# react基础

## 创建项目

1. 安装脚手架：npm install -g create React App
2. 创建项目：npx create-react-app my-app(npx create-react-app@latest your-project-name --use-npm)
3. cd my-app npm start

## JSX

### 优点：

1. jsx 执行更快，编译为 js 代码时进行了优化
2. 类型更安全，编译过程如果出错就不能编译，及时发现错误
3. jsx 编写模板更加简单快速

### 注意：

1. jsx 必须要有根节点。
2. 正常的 html 元素要小写、如果大写，默认认为是组件

### 语法规则

1. 定义虚拟 dom 时不要写引号。
2. 标签中混入 js 表达式要用{}
3. 样式的类名指定不要用 class 要用 className
4. 内联样式，要用 style={{key:value}}的形式写
5. 只有一个根标签
6. 标签必须闭合
7. 标签首字母:
8. 若小写字母开头则将标签转为 html 中同名元素，若 html 中无该标签的同名元素则报错。
9. 若大写字母开头，react 就去渲染对应的组件，若组件没有定义则报错

### ReactDOM.render

- 函数式组件
  - React 解析组件标签，找到对应组件。
  - 发现组件是使用函数定义的，随后调用该函数，将返回的虚拟 DOM 转化为真实 DOM，随后呈现在页面中
- 类组件
  - React 解析组件标签，找到对应组件。
  - 发现组件是类定义的，随后 new 出该类的实例，调用到原型上的 render 方法。
  - 将 render 返回的虚拟 DOM 转化为真实 DOM，随后呈现到页面中。

### 回调形式的 ref 调用次数

1. 如果回调形式的 ref 使用内联函数的形式定义的，则在更新过程中会被调用两次
2. 如果写成一个类绑定形式的函数则只会调用一次

### React.createRef()

- 调用后可以返回一个容器，盖容器可以存储被 ref 所标识的节点,盖容器是专人专用

### 事件处理

```Plaintext
1.通过onXxx属性指定事件处理函数(注意大小写)
    1 React使用的是自定义(合成)事件, 而不是使用的原生DOM事件---为了更好的兼容性
    2 React中的事件是通过事件委托方式处理的(委托给组件最外层的元素)---为了更高效
2.通过event.target得到发生事件的DOM元素对象---不要过度使用ref
```

### 受控组件与非受控组件

- 现用先取是非受控，输入标单项受 state 是受控组件

### 高阶函数与函数的柯里化

- 高阶函数：如果一个函数符合下面两个规范中的任何一个，那么这个函数就是高阶函数
- 若函数 A，接收一个参数是函数，那么 A 就可以成为高阶函数
- 若函数 A，调用的返回值依然是一个函数，那么 A 就可以称之为高阶函数
- 如：Promise，定时器，map，filter
- 函数柯里化：通过函数调用继续返回函数的方式，实现多次接收参数最后统一处理的函数编码形式

### 父子组件传值

1. 父组件给子组件传递数据：通过 props
2. 子组件给父组件传递数据：通过 props，要求父组件提前给子组件传递一个函数

### 路由组件与一般组件

1. 写法不同:一般组件 路由组件:

```
<Route path="/about" component={About} />
```

1. 位置不同:一般组件放在 components 中 路由组件存放在 pages 中
2. 接收到的 props 不同:一般组件：写组件时传入了什么，就能收到什么。路由组件：接收到三个固定的属性

## react 组件

1. 函数式组件
2. 类组件
3. 复合组件：组件中又有其他组件，复合组件中既可以有类组件又可以有函数式组件函数式与类组件的区别：函数式组件比较简单，一般用于没有交互内容的组件页面，类组件，一般又称为动态组件，那么一般会有交互或者数据修改的操作。

## react State

- 相当与 vue 的 data 但是使用方式和 vue 不一样

## props

- 父传递给子组件的数据，单向流动，不能传递给父。 props 的传值可以是任意的类型。 props 可以设置默认值 HelloMessage.defaultProps = { name: "duke" } 注意：props 可以传递父元素的函数，就可以去修改父元素的 state，从而达到传递数据给父元素。

## React 数据传递

### 子传父

- 调用父元素的函数从而操作父元素的数据，从而实现数据从子元素传递至父元素

### 父组件调用子组件的方法

```TypeScript
import {useRef, useImperativeHandle} from "react"
const Child =(props)=>{
  const childFunc = () =>{
    console.log("我是自子组件的方法")
  }
  /**提供给父组件调用 */
  useImperativeHandle(props.onRef, () => {
    // 需要将暴露的接口返回出去
    return {
      func: childFunc,
    };
  });
  return <div>我是子组件</div>
const Parent = ()=>{
  const childRef = useRef()
  const handleOnClick = () => {
    if (BillRef.current && BillRef.current.func) {
      BillRef.current.func();
    }
  };
  return (
    <div>
      <Child onRef={BillRef}/>
      <buttom onClick={handleOnClick}>点击</buttom>
    </div>
  )
}
```

## React 事件

- 特点：

1. react 事件，绑定事件的命名，驼峰命名法。
2. {}，传入一个函数事件对象：React 返回的事件对象是代理的原生事件对象，如果想要查看事件对象的具体值，必须直接输出事件对象的属性原生，阻止默认行为，可以直接返回 return false使用匿名箭头函数传递参数

## 生命周期

- 生命周期即是组件从实例化到最终从页面中销毁，整个过程就是生命周期，在这生命周期中，我们有许多可以调用的事件，也俗称钩子函数生命周期的三个状态： Mounting:将组建插入到 DOM 中 Updating:将数据更新到 DOM 中 Unmounting:将组建移除 DOM 中
- 生命周期中的钩子(方法，事件) ComponentWillMount:组件将要渲染,AJAX ComponentDidMount:组件渲染完毕.添加动画 componentWillReceiveProps: 即将过时，组件将要接收 props 的数据，查看接收的 props 的数据是什么 ShouldComponentUpdate:在组件接收到新的 state 或者 props，判断是否要更新。返回 boole 值 CompontentWillUpdate：组件将要更新 ComponentDidUpdate:组件已经更新 ComponentWillUnmounted:组件将要卸载
- 兄弟组件传值 pubsub-js

## 浏览器跨域

1. 正向代理--正常开发 一个位于客户端和目标服务器之间的代理服务器，为了获取到目标服务器的内容，客户端向代理服务器发送一个请求 代理服务器帮助我们去目标服务器里面获取数据并且返回给我们
2. 反向代理--生产环境 可以通过代理服务器来接收网络上的请求链接 然后将这个请求转发给内部的服务器上 并且把这个服务器上的道德数据返回给网络请求的客户端 这个时候代理服务器对外的表现就是一个反向代理

```
node_modules-->react-script-->config-->webpackDevServer.config.js: proxy:{ target: "目标地址", changeOrigin: true, pathRewrite:{ "^/api": "/" } }
```

## 路由

react-router-dom

# [github地址](https://github.com/7kms/react-illustration-series)