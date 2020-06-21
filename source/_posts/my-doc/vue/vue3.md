# Vue3

## 升级内容

- 全部用TS重写

- 性能提升，代码量减少

- 会调整部分API



## Proxy实现响应式

- 回顾Object.defineProperty

  - 深度监听，需要一次性递归完成。而Proxy是get之后才会进行下一层的Proxy监听
  - 无法监听新增，删除Vue.set,Vue.delete

  

### 基本使用

![image-20200620113336646](F:\my-code\my-blog\Blog\source\_posts\my-doc\vue\vue3-images\image-20200620113336646.png)



### Reflect

- 和Proxy能力对应
- 规范化，标准化、函数式
- 代替Object上面的API



### 实现响应式

- 深度监听
  - 需要递归。但是是只有获取时才会去递归下一层。
  - 但是性能如何提升的？
    - Proxy是当对象get之后，才会进行下一层的监听。而ObjectdefineProperty是一次性就observal完成。
- 数组监听
  - 数组实际也是一个对象{0:'a',1:'b'}，所以能实现
- 新增删除
  - 新增：set
  - 获取：get
  - 删除：deleteProperty
- 缺点：
  - 无法兼容所有浏览器。

