# 种子模块

## 对象扩展

解决问题：新功能添加到我们的命名空间

任务：

- $.mix实现
- Object.assign实现

## 数组化

arguments，document.forms等获取节点集合，实际是用类的方式实现的，不是一个数组。

- 用slice来实现   

  - ```javascript
    var a = {0:"a",1:"b",length:2}
    Array.prototype.slice.call(a,0,2)
    ```

- `Array.from({})`

## 类型判断

- isNull

- isUndefined

- isString

- isNumber

- isBoolean

- isSymbol

- isDate

- isRegExp

- isArray

- isArrayLike （比较复杂，jQuery没有暴露出来）

- isWindow

  - ```javascript
    obj!==null && obj.window == obj
    ```

- isNaN

- isPlainObject

  - ```javascript
    typeof obj === "object" && Object.getPrototypeOf(obj) === Object.prototype
    ```

  

可以发现，这种类型的判断越来越多。核心原则：

- 基础类型可以通过`typeof`来判断
- 其他类型通过 `Object.prototype.toString.call(obj)`
- 特殊类型，`isWindow，isNaN，isPlanObject，isArrayLike` 要靠其他办法





## 无冲突处理

使用：

1. 引用其他库比如：这个库也用了$，作为使用方式，那么就会冲突
2. `var _ = $.noConflict()`;//改名操作，这里返回的是jQuery

## `DOMReady`

是`DOMContentLoad`的一种别称，由于框架需要，与原生的`DOMContentLoad`有一点区别。

>  `window.onload` 触发条件是资源文件如图片都加载完成才会触发，而框架所要做的是尽快

实现：

```
d.onreadystatechange = function(){
    if(d.readyState === "complete"){
        d.onreadystatechange = null
        init()//执行初始化代码
    }
}
```

问题：如果代码是动态加载的呢？，也就是说不会触发`onreadystatechange`，`jQuery`的做法是 `onload`也一起监听，然后判断`document.readyState === "complete"`



# `MVVM`

## 前端模板（静态模板）

比较强大的：nunjucks

1. 用slice+indexOf来实现一个简单模板
2. 用JSON.stringify 来添加双引号
3. dig和fill方法，来为变量添加前缀： data.info  + data.message
4. 模板中 if，for的处理
   1. 使用with来处理i，el等这种临时变量（）
   2. 使用新的语法（性能更好）
5. 如何区分while，dowhile，else等

## MVVM的动态模板

静态模板的缺陷：

- 破坏了对事件的绑定
- 破坏了原来区域的 选区和光标
- 破坏了原区域的第三 方组件

MVVM架构：

- 最小化刷新
- 性能大幅度提升



[解析模板中 inline 的表达式两种方式](<https://www.zhihu.com/question/29743491/answer/49301464>)：

- 正则提取，使用with
- 使用 parser



一个绑定属性至少包括**类型**（比如：text绑定）与表**达式**（`text:a`）两部分，所有指令都会转换为一个绑定对象

绑定对象：

- type类型（比如：text绑定）
- expr表达式
- element目标元素
- param额外传参
- filters过滤器
- vm（扫描时获取的数据集合）对象



### 变量抽取（双向绑定）

将`data-bind="text:name"`表达式里面的值，变量全部抽取出来，用来做依赖收集。

变量抽取是为了动态依赖收集服务。动态依赖，要求对求值函数进行深 改造。触发getter，

所以vm的属性 必须是get，set 或者和ko一样是一个函数 。

### vm对象路径抽取

angular采用的方式

![1588001313518](F:\my-code\my-blog\Blog\source\_posts\my-doc\读书笔记\js框架设计\js框架设计\1588001313518.png)



### 刷新函数（指令）

刷新函数是内置的视图刷新方法，有多少种指令，就有多少种刷新方法

##### 逻辑指令

- if
- for
- ...

##### 普通指令

- attr
- css
- click
- ...

##### 指令中的锚点系统

比如 if，为真时，渲染元素，为假时。移除dom。。再次为真，则通过这个锚点来重新插入



有的MVVM没有生成锚点，直接用空白节点，这个需要 浏览器兼容性比较好 。

其实空白节点和注释节点性能是一样的。只是用户看起来，很牛逼，不会有些奇怪的注释代码在上面

空白节点是可以添加属性的：

```
var anchor = document.createTextNode('');
anchor.xxx = '$key,$val in @object';
在IE6-8，空白节点操作属性会失效
```

##### 锚点系统和diff算法

![1588002325166](F:\my-code\my-blog\Blog\source\_posts\my-doc\读书笔记\js框架设计\js框架设计\1588002325166.png)



### 事件和duplex（双向绑定）

事件的问题 ：要求求值函数 ，必须总是返回同一个函数，解决办法：uuid的事件系统



## ViewModel

按照原型 连长度来划分对象：

- 超轻量：Object.create(null)
- 轻量{}
- 重量，有一到二重，或带有属性访问器的对象。avalon或vue的vm
- 超重量   

实现Object.defineProperty的几种方案：



##### Proxy



##### Reflect



## React与虚拟dom

React的diff算法

React的多端渲染



## 性能墙与复杂墙

什么是性能墙与复杂度墙？
https://www.zhihu.com/question/40195289/answer/85321338

[迷你html-parser](<https://github.com/lemonde/cms-htmlparser>)



参考：

- [如何理解虚拟DOM](<https://www.zhihu.com/question/29504639>)
- [虚拟dom  vs 原生 dom](<https://www.zhihu.com/question/31809713>)
- [avalon如何在 ie的兼容情况下做到双向 绑定](<https://www.zhihu.com/question/42001493>)
- <https://ww.cnblogs.com/DebugLZQ/archive/2012/05/15/2501512%20.html>
- <https://www.jianshu.com/p/9a6845b26856>
- 





