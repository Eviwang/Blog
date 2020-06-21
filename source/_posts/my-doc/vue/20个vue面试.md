20个面试题

# Vue

## v-show 和v-if的区别

- v-show 通过控制CSS  display控制显示和隐藏
- v-if组件真正的渲染和销毁，而不是显示和隐藏
- 频繁切换显示状态用v-show，否则用v-if

## 为何v-for中要用key

- 必须用key，且不能是index和random
- diff算法中通过tag和key来判断，是否是sameNode
- 减少渲染次数，提升渲染性能

## 描述Vue组件生命周期（有父子情况）

- 单组件生命周期
- 父子组件生命周期关系

## Vue组件如何通讯

- 父子props和this.$emit
- 自定义事件 event.$on,event.$off,event.$emit
- vuex
- provider,inject
- this.$parent 可以直接拿到父组件。

## 组件渲染和更新的过程



## 双向数据绑定的v-model的实现原理

- input 元素的value = this.name
- 绑定input事件this.name = $event.target.value
- data更新触发re-render

## computed 有何特点

- 缓存，data不会重新计算
- 提高性能

## 为何组件data必须是一个函数

如果是对象，引用类型。在渲染多个组件的话，会相互影响。

## ajax请求应该放在哪个生命周期

- mounted
- js是单线程的，ajax异步获取数据
- 放在mounted之前没用，只会让逻辑更加混乱

## 如何将组件所有props传递给子组件？

- $props
- `<User v-bind="$props"/>`

## 如何自己实现 v-model



## 多个组件有相同的逻辑，如何抽离？

- mixin
- mixin的缺点？



## 何时使用异步组件？

- 加载大组件
- 路由异步组件



## 何时使用keep-alive？

- 缓存组件，不需要重复渲染。
- 多个静态tab页的切换
- 优化性能

## 何时需要使用beforeDestory

- 解绑自定义事件 event.$off
- 清除定时器
- 解绑自定义的DOM事件，如window scroll



## 什么是作用域插槽

![image-20200620110729462](F:\my-code\my-blog\Blog\source\_posts\my-doc\vue\20个vue面试-images\image-20200620110729462.png)



## Vuex中action和mutation有何区别

- action中处理异步，mutaion不可以
- mutaion做原子操作
- action可以整合多个mutaion

## Vue -router 常用的路由模式

- hash（默认）
- H5 history（需要服务端支持）

## 如何配置Vue-router异步加载

![image-20200620111044969](F:\my-code\my-blog\Blog\source\_posts\my-doc\vue\20个vue面试-images\image-20200620111044969.png)



## 用vnode描述一个DOM结构

![image-20200620111149141](F:\my-code\my-blog\Blog\source\_posts\my-doc\vue\20个vue面试-images\image-20200620111149141.png)

## 监听data变化的核心API是什么

- Object.defineProperty
- 深度监听、数组监听
- 缺点

## Vue如何监听数组变化

- Object.defineProperty不能监听数组变化
- 重新定义原型，重现push pop等方法，实现监听
- Proxy可以原生支持监听数组变化

## 描述响应式原理

- 监听data变化

- 组件渲染和更新的流程

## diff算法的时间复杂度

- O（n）
- 在O（n3）的基础上优化

## 简述diff算法的过程

- patch
- patchVnode和addVnodes和removeVnodes
- updateChildren（key的重要性）



## Vue为何是异步渲染，$nextTick何用

- 异步渲染（合并data修改），以提高渲染性能
- $nextTick在DOM更新完之后，触发回调

## Vue常见性能优化方式

- 合理使用v-if v-show
- 合理使用 computed
- v-for时加key，以避免v-if同时使用
- 自定义事件，dom事件及时销毁
- 合理使用异步组件
- 合理使用keep-alive
- data层级不要太深
- 使用vue-loader在开发环境做编译
- webpack层面优化
- 前端通用性能优化，图片懒加载
- 使用SSR





# React

## React组件如何通讯



## JSX的本质是什么



## context是什么，有何用途



## shouldComponentUpdate的用途



## 描述redux的单项数据流



## setState是同步还是异步







# 框架综合应用

## 基于React设计一个todoList（组件结构，redux state数据结构）



## 基于Vue设计一个购物车（组件结构，vuex state的数据结构）



# webpack 面试题



## 前端代码为何需要进行构建和打包



## module chunk bundle分别是什么意思，有何区别



## loader和plugin的区别



## webpack如何实现懒加载



## webpack常见性能优化



## babel-runtime和babel-polyfill 的区别



# 如何应对上述面试题



## 框架的使用（基本使用，高级特性，周边插件）



## 框架的原理（基本原理的了解，热门技术的深度，全面性）



## 框架的实际应用，设计能力（组件结构，数据结构）





# 面试官为何要这样考察？

## 保证候选人正常工作-考察使用

## 多个候选人竞争时，选择有技术追求的-考察原理

## 看候选人是否能独立承担项目-考察设计能力





# 

