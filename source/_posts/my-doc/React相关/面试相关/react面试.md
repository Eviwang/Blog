# 基本使用 

jsx语法

条件

列表渲染

事件

- bind this
- 关于event参数
  - react中的event是`Synthetic Event`,所有的事件都被挂载到document上
  - `event.nativeEvent` 才是原生事件对象
- 传递自定义参数

组件和props

state和setState

- 不可变

- 可能同步

  - 在同步操作中是异步

    - ```javascript
      this.setState({count:1});console.log(this.state.cout)
      ```

  - 如果传入回调函数（第二个参数）则在回调中能拿到返回值

  - 异步操作中是同步（setTimeOut,dom事件）

- 可能合并

  - 合并（覆盖）情况

    - ```javascript
      this.setState({count:this.state.count+1})
      ```

  - 不合并（覆盖）情况

    - ```javascript
      this.setState((state,props)=>{ 
          return  {
              count:state.count + 1    
          }
      )
      ```

      

组件生命周期

<http://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/>



# 高级特性

### 函数组件

### 非受控组件

1. 使用`defaultValue`来赋初始值，使用ref来显示value。

- refs

- defaultValue 

  - ```jsx
    <input defaultValue="test" ref={}/>
    ```

- defaultChecked

2. 使用场景：

- 必须手动操作dom元素，setState实现不了
- 比如文件上传 `<input  type="file"/>`
- 富文本 编辑器

3. 使用原则：

- 优先使用受控组件
- 必须操作DOM，使用非受控组件

### Portals

- 组件默认会按照层次嵌套渲染
- 如何让组件渲染到父组件以外

使用场景：

- `overflow:hidden`
- 父组件z-index值太小
- fixed需要放在body第一层

### context

如何定义？

解决什么问题？

- 跨组件通信
- 应对逻辑不复杂的情况

函数组件怎么消费 

```jsx
<ThemeContext.Consumer>{(value)=><p>{value}</p>}</ThemeContext.Consumer>
```

类组件怎么消费

```jsx
class  ThemeButton extends React.Component{
    static contextType = ThemeContext
    render(){
        return <div>{this.context.theme}</div>
    }
}
```



### 异步组件

```jsx
const Demo React.lazy(import("../demo"));

// 使用
<React.Suspense fallback={<div>loading...</div>}>
	<Demo/>
</React.Suspense>
```





## 性能优化（重要）

## 1. shouldComponentUpdate

- **性能优化，永远都是面试的重点**
- 性能优化对于React更加重要
- 回顾setState时强调不可变值

1. `shouldComponentUpdate`

   1. **更深一层讨论，为什么 React默认不帮我们来实现对比？**

   2. React默认：父组件有更新，子组件无条件更新。

   3. SCU一定要每次都用吗？  **需要的时候才优化** 。

   4. 使用 `_.isEqual(nextPropos.list,this.props.list)`来进行深度比较。

   5. `shouldComponentUpdate`一定要配合不可变值来使用。因为对比的时候回有问题：

      错误方式：直接push了，那么`setState`的时候，两个值相等了，会导致，`shouldComponentUpdate`对比时，不会更新。

![1587564033702](F:\my-code\my-blog\Blog\source\_posts\my-doc\React相关\面试相关\react面试\1587564033702.png)

总结：

- SCU默认返回true，即React默认重新渲染所有子组件
- 必须配合“不可变值 ”一起使用
- 可先不用SCU，有性能问题时再考虑使用

1. `PureComponent` 和 React.memo
2. 不可变值immutable.js

## 2. 纯组件和React.memo

默认实现了浅比较

## 3. 不可变值 immutablejs

- 彻底拥抱“不可变值”

## 关于组件公共 逻辑的抽离

## 1. 高阶组件HOC

## 2. Render Props

核心思想：通过一个函数将`class`组件的state作为props传递给纯函数组件。

## 3. HOC VS Render Props

- hoc 模式简单，但会增加组件层级
- Render Props：代码简洁，学习成本较高
- 按需使用



## Redux 使用

- 和Vuex作用相同，但比Vuex学习成本高
- 不可变值，纯函数 
- 面试常考

### 基本使用

- 基本 概念
  - store state
  - action
  - reducer
- 单项数据流(常考，画出来)【同步和异步】
  - dispatch(action)
  - reducer -> newState
  - subscribe 触发更新
- `react-redux`
  - Provider
  - connect
  - `mapStateToProps`,`mapDispatchToProps`
- 异步action
  - react-thunk
  - react-saga
  - react-promise
- 中间件

![1587566373125](F:\my-code\my-blog\Blog\source\_posts\my-doc\React相关\面试相关\react面试\1587566373125.png)

- 中间件是加在  dispatch 层的 

- reducer是纯函数
- view纯展示

![1587566530359](F:\my-code\my-blog\Blog\source\_posts\my-doc\React相关\面试相关\react面试\1587566530359.png)

## React-Router

- 面试考点并不多（前提是熟悉React）

- 路由模式（hash、H5 history）

  - 默认hash
  - history
  - 后者需要server支持 

- 路由配置（动态路由、懒加载）

  - `const { id } = useParams()`,`userHistory()`

  - 懒加载：

    ```jsx
    const Home = lazy(()=>import("./routes/home"))
    <Router>
    	<Suspense fallback={<div>test</div>}>
        	<Route></Route>
        </Suspense>		
    </Router>
    ```

    

# 原理

### 函数式编程

- 一种编程范式，概念比较多
- 纯函数
- 不可变值

###  `vdom`和`diff`

### `JSX`本质

### 合成事件

![1587569009383](F:\my-code\my-blog\Blog\source\_posts\my-doc\React相关\面试相关\react面试\1587569009383.png)

  - - 为什么要用合成事件？ 
    - 为了更好的兼容性和跨平台
    - 挂载到document，减少内存消耗
    - 方便事件的统一管理（如事务机制）

- `setState` `batchUpdate`

- 组件渲染过程

- 前端路由原理

  

### `setState`和`batchUpdate`

- setState主流程
- batchUpdate机制
- transaction机制

![1587646482022](F:\my-code\my-blog\Blog\source\_posts\my-doc\React相关\面试相关\react面试\1587646482022.png)

![1587646692812](F:\my-code\my-blog\Blog\source\_posts\my-doc\React相关\面试相关\react面试\1587646692812.png)

事件监听中：

![1587646733008](F:\my-code\my-blog\Blog\source\_posts\my-doc\React相关\面试相关\react面试\1587646733008.png)

`setState`异步还是同步？

- `setState`无所谓异步还是同步
- 看是否能命中`batchUpdate`机制
- 主要是判断`isBatchingUpdate`

那些能命中`batchUpdate`机制（异步）

- 生命周期（和它调用的函数）
- React中注册的事件（和它调用的函数）onClick，onChange
- React可以“管理”的入口

那些不能命中`batchUpdate`机制（同步）

-  `setTimeout` `setInterval`等（和它调用的函数）
- 自定义DOM事件（和它调用的函数）
- React 管不到的入口

### transaction事务机制

![1587647149668](F:\my-code\my-blog\Blog\source\_posts\my-doc\React相关\面试相关\react面试\1587647149668.png)

![1587647274077](F:\my-code\my-blog\Blog\source\_posts\my-doc\React相关\面试相关\react面试\1587647274077.png)

#### 面试考点

- jsx如何渲染为页面 
  - JSX 即 createElement函数
  - 执行生成vnode
  - patch（ele，vnode）和patch（vnode，newVnode）
- `setState`之后如何更新页面
- 面试考察全 流程

#### 组件更新过程

- `setState -> dirtyComponents`(可能有子组件)
- `render()` 生成 `newVnode`
- `patch(vnode,newVnode)`

#### 更新的两个阶段

- patch分为两个阶段：
- reconciliation阶段-执行 `diff` 算法，纯`js`计算 （可以被中断）
- commit阶段-将diff结果渲染到dom（不会被中断）

为什么 分为两个阶段？

- js是单线程，且和DOM渲染公用一个线程
- 当组件足够复杂，组件更新时计算和渲染都压力大
- 同时再有DOM操作需求（动画，鼠标拖拽）将卡顿

解决办法：fiber

- 将reconciliation阶段拆分
- DOM需要渲染时暂停，空闲时恢复
- window.requestIdleCallback



# 面试真题

## 组件之间如何通信

- 父子组件props
- 自定义 事件
- Redux
- React.Context

## JSX本质是什么

- createElement
- 执行返回vnode

## Context是什么，如何应用

- 父组件，向下所有子孙组件传递信息
- 如一些简单的公共信息：主题色、语言等
- 复杂的公共信息，请用redux

## `shouldComponentUpdate`的用途

- 性能优化
- 配合不变值一起使用

## `redux`单项数据流

（画图）

## setState场景题

![1587648702577](F:\my-code\my-blog\Blog\source\_posts\my-doc\React相关\面试相关\react面试\1587648702577.png)

## 什么是纯函数

- 返回一个新值，没有副作用
- 重点：不可变值
- 如arr = arr.slice()

## React发起ajax应该放在哪个生命周期 ？

- `componentDidMount`

## 列表渲染 ，为何使用key

- 必须使用key，且不能是index和random
- diff算法中通过tag和key来判断，是否是sameNode
- 减少渲染次数，提升渲染性能

## 函数组件和class组件区别

-  纯函数，输入props，输出jsx
- 没有实例生命周期，没有state
- 不能扩展其他方法

## 什么是受控组件

- 表单的值，受state控制
- 需要自行监听onChange，更新state
- 对比非受控组件

何时使用异步组件

- 加载大组件
- 路由懒加载

多个组件有公共逻辑 ，如何抽离 

- 高阶组件HOC
- Render Props
- mixin已经被废弃

redux如何进行异步请求

- 使用异步action
- 如`redux-thunk`

react-router如何配置懒加载

![1587649183748](F:\my-code\my-blog\Blog\source\_posts\my-doc\React相关\面试相关\react面试\1587649183748.png)

PureComponent有何区别

- 实现了浅层比较
- 性能优化
- 要结合不可变值使用

React事件和DOM事件区别 

- 所有事件挂载到document上
- event不是原生的，是SyntheticEvent合成事件对象
- dispatchEvent 机制（忘了）

React性能优化

- 渲染列表时加key
- 自定义事件、DOM事件及时销毁
- 合理使用异步组件
- 减少函数bind this的次数
- 合理使用SCU PureComponent和memo
- 合理使用Immutable.js
- webpack层面的优化
- 前端通用的性能优化 、如图片懒加载 
- 使用SSR

React和Vue的区别

- 都支持组件化
- 都是数据驱动视图
- 都是vdom操作DOM
- React使用JSX拥抱JS，vue使用模板拥抱html
- React函数式编程，Vue声明式编程
- React更多需要自力更生，Vue把想要的都给你 （初学者很友好）