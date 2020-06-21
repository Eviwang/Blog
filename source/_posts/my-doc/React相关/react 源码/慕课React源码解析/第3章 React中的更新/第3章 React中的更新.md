创建更新的三种方式

- ReactDOM.render || hydrate(服务端渲染)
- setState
- forceUpdate



步骤：

1. 创建 ReactRoot
2. 创建 FiberRoot和RootFiber
3. 创建更新（下一章）



## 3-1 react-dom-render

代码在：`react-dom/src/client`



##  3-2 react-fiber-root

##  3-3 react-fiber

##  3-4 react-update-and-updateQueue

什么是update？

- 用于记录组件状态的改变
- 存放于UpdateQueue中
- 多个Update可以同时存在





##  3-5 react-expiration-time

##  3-6 different-expirtation-time

##  3-7 react-setState-forceUpdate