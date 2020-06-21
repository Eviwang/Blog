# Vue使用



## 基本使用，组件使用-常用，必须会

- 插值，表达式
- 指令，动态属性
- v-html：会有XSS风险，会覆盖子组件



### computed和watch

- computed有缓存，data不变则不会重现计算

- watch如何深度监听

  ```
  watch:{
      info:{
          handler(old,val){
              
          },
          deep:true
      }
  }
  ```

  

- watch监听引用类型
  注意情况：

  - 如果改变的是对象内部的属性则，old和newVal是同一个对象

  - 如果直接被覆盖了，则old和new不是一个对象

```java
 methods: {
    changeVal() {
      this.info.user = 'jerry';
      // this.info = {
      //   user: '333',
      // };
    },
  },
  watch: {
    info: {
      handler(old, newVal) {
        console.log(old === newVal);
      },
      deep: true,
    },
  },
```



### class 和 style

- 使用动态属性
  - 对象
  - 数组
- style绑定使用驼峰式写法

![1591875776568](F:\my-code\my-blog\Blog\source\_posts\my-doc\vue\vue-images\1591875776568.png)



### 条件渲染

- v-if v-else的用法，可以使用变量，也可以使用===表达式
- v-if和v-show的区别
  - 频繁切换用v-show
- v-if和v-show的场景



### 循环渲染

- 如何遍历对象？  也可以用v-for
- key的重要性。key不能乱写
- v-for和v-if  在同一个元素上是不能一起使用
  - v-for比v-if的优先级高





### 事件

vue的事件是原生的事件，事件是被挂载到当前元素上面。

- event参数，自定义参数

  - `@click="increament"`当increment接受时，第一个参数是event
  - `@click="increament(22,$event)"`自定义参数

- 事件修饰符，按键修饰符

  ![1591876630939](F:\my-code\my-blog\Blog\source\_posts\my-doc\vue\vue-images\1591876630939.png)

- 【观察】事件被绑定在哪里？

  事件是被挂载到当前元素上面。



### 表单（考察的不多）

- v-model
- 常见表单项 textarea checkbox radio select



### Vue 组件使用

- 父子通讯：props和$emit
- 兄弟通讯：组件通讯-自定义事件
  - 需要有个event库。默认  `eventbus = new Vue()`
    - event.$on('',fn)
    - event.$off
    - event.$emit('')
- 组件生命周期
  - beforeCreate
  - created
  - `beforeDestroy()` 销毁绑定事件。







## 高级特性-不常用，但体现深度





## `Vuex `和 `Vue-router`使用





