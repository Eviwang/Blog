# Vue



形成闭环，不是说为了面试而面试，更多的是考察工作中的运用。不会刻意刁难面试者





## 组件化



## 响应式

- `Object.defineProperty`

  - 监听对象

    - 新增属性 `this.set()`
    - 删除属性`this.delete()`

  - 监听数组

    - 对原型链进行拦截：先更新视图，然后，调用原生的数组方法：

      ```javascript
      const oldArrayPrototype = Array.prototype
      const arrProto =  Object.create(oldArrayPrototype);
      ['push','pop','shift','unshift'].forEach(methodName=>{
      	arrProto[methodName]= function(){
      	    // 触发更新
      		updateView();
      		// 调用原生的方法
      		oldArrayPrototype[methodName].call(this,...arguments)
      	}
      });
      
      // 在observer()方法里面，将原型链改为，重写后的
      if(Array.isArray(target)){
         target.__proto__ = arrProto;
      }
      ```

      

  - 复杂对象深度监听

    - 深度遍历进行监听

  - 几个缺点

    - 深度监听，需要递归到底，一次性计算量大
    - 无法实现新增，删除

- Proxy



## `vdom`和`diff`

### 应用背景

- DOM操作非常耗时（诞生原因）
- 以前的`jQuery`，可以自行控制DOM操作的时机，手动调整
- `Vue`和React是数据驱动视图，如何 有效控制DOM操作？



解决方案：

- 将`dom`计算转换为JS计算，JS执行快。
- `vdom`，来模拟DOM结构，计算出最小的变更，操作DOM

### vnode结构 

### `snabbdom` 的使用：`vnode h patch`



### diff 算法

- diff算法是一个比较广泛的概念，如linux diff，gitdiff
- 两个js对象也可以做diff，如： https://github.com/cujojs/jiff
- 两课树做`diff`。前端`diff`算法

树的diff算法复杂度 O(n3)

优化时间复杂度到O（n）

- 只比较同一层，不跨级比较
- tag不同，则直接删掉重建，不再深度比较
- tag和key，两者都相同，则认为是相同节点，不再深度比较。



将my- React 写一遍就懂了。



## 模板编译

- 它不是html，有指令，插值，js表达式，到底是什么？
- 面试不会直接问，但会通过“组件渲染和更新过程”考察



- with语法：

  ![image-20200619231554326](F:\my-code\my-blog\Blog\source\_posts\my-doc\vue\vue原理-images\image-20200619231554326.png)

- vue template compiler将模板编译为render函数
- 执行render函数生成vnode



-  模板不是html，只有指令、插值，JS表达式，能实现判断、循环
- html是标签语言，只有JS才能实现判断、循环（图灵完备的语言）

### `vue-template-compiler`



- 模板会编译为render函数，执行render函数返回vnode
- 基于`vnode`再执行`diff`
- 使用`webpack vue-loader` 会在开发环境进行编译。

### 总结：

- 响应式：监听data属性getter setter
- 模板编译:从模板到render函数，再到vnode
- `vdom`: patch(el,vnode) 和 patch(vnode,newVnode)



## 渲染过程

### 初次渲染过程

- 解析模板为render函数，（开发环境，`vue-loader`处理了）
- 触发响应式，监听data属性getter setter
- 执行render函数，生成`vnode`，`patch(el,vnode)`

### 更新过程

- 修改data，触发setter
- 重新执行render函数，生成newVnode
- patch（`vnode`，`newVnode`）

### 异步渲染

- `$nextTick`
- 汇总data的修改，一次性更新视图
- 减少DOM操作次数，提高性能

## 前端路由

### hash特点

- hash变化会触发网页跳转，即前进后退
- hash变化不会刷新页面，spa 必须的特点
- hash永远不会提交到server端。

### hash触发条件

- `js`   
  - `location.href= "#/test"`
  - `location.hash = "pageA"`
- 手动
- 浏览器前进后退



### `H5 history`（需要server端配合）

- `url`规范的路由，跳转时不刷新页面
- `history.pushState(state,null,'pageA')`
- `window.onpopstate(event)`



### 选择

- to B的系统推荐hash，简单易用，对url规范不敏感
- to C的系统，可以考虑H5 history，但需要服务器支持
- 能选择简单的，就别用复杂的，要考虑成本和收益。不要为了技术设计而设计







