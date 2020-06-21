# Angular 核心概念

## cli

`ng build --prod`





## 三大核心概念

- Component
- Module
- Route

### Component

单项数据流



angular模块生成器，可以生产一个组件树



chrome插件：

Augury



模块依赖查看器

[ngd](<https://github.com/compodoc/ngd>)



### NgModule

angular中，一切以模块为单位。

一个类加上装饰器就是一个NgModule了。

```javascript
@NgModule({
  declarations: [AppComponent],// 那些属于本 NgModule 的组件、指令、管道
  imports: [BrowserModule, AppRoutingModule, HomeModule],
  providers: [],// 本模块向全局服务中贡献的那些服务的创建器
  bootstrap: [AppComponent],//根模块启动项
  exports: [ListComponent], //那些能在其它模块的组件模板中使用的可声明对象的子集，不导出，别人没法使用 
})
```

[为什么需要NgModule](<https://www.zhihu.com/question/376817427>)







### Router



## 整体架构

### 依赖注入

  provider中注明，然后在组件中注入



### 数据绑定

Imutable



## UI库 

- PrimeNG（推荐）
- NG-Zorro （推荐）
- Jigsaw
- Clarity （还可以 ）
- Angular-Material 组件少，更新慢，功能少
- Ionic（移动端）

## 参考资源

- ngx-admin
- JHipster
- [angulardoc.org ](<https://angulardoc.org/>) 资料库



#  Angular版本升级

- lvy render 打包优化
- vscode 直接debug angular



# 组件

### 基础

- scss

- 插值语法和表达式



- 模板内定义局部变量

  模板可以调用方法

  用#号定义dom变量，在方法中可以直接引用这个dom

  ![1583761069433](F:\my-code\my-blog\Blog\source\_posts\my-doc\angular\angular-damo\1583761069433.png)

- 值绑定[]、事件绑定()、双向绑定`[()]`

- 内置结构指令用法： `*ngIf` *ngFor ngSwitch

  - ngIf是直接删除 dom
- 内置属性指令 NgClass 绑定一个对象 ，NgStyle NgModel   [(ngModel)]
- 小工具：管道、安全导航、非空断言

  - `current?.value` angular 模板中支持

### 通信

- 父子

  - @Input  【get,set】可以利用set作为subscrible

  利用`#定义变量`直接调用子组件的方法。

  ![1583762395059](F:\my-code\my-blog\Blog\source\_posts\my-doc\angular\angular-damo\1583762395059.png)

  - @output  

  ```@output aa = new EventEmitter()```

  - 模板变量
  - @ViewChild

- 兄弟或者没有直接关系

  - 新建一个event-bus.service.ts，然后 两个组件中都注入

  ![1583762560538](F:\my-code\my-blog\Blog\source\_posts\my-doc\angular\angular-damo\1583762560538.png)

- 没有直接关系

  - service/localstorage   共享service
  - session/路由参数

### 生命周期

- 生命周期钩子概述

  check相关的会调用多次，所以 不要做复杂的逻辑，1的是只会调用一次

  - constructor
  - ngOnChanges *
  - ngOnInit   (1)
  - ngDoCheck *
    - ngAfterContentInit  (1)
    - ngAfterContentChecked *
    - ngAfterViewInit   (1)
    - ngAfterViewChecked *
  - ngOnDestory  (1)

![1583763124784](F:\my-code\my-blog\Blog\source\_posts\my-doc\angular\angular-damo\1583763124784.png)



![1583763132052](F:\my-code\my-blog\Blog\source\_posts\my-doc\angular\angular-damo\1583763132052.png)

### 指令和组件的关系

![1583763211535](F:\my-code\my-blog\Blog\source\_posts\my-doc\angular\angular-damo\1583763211535.png)



- ngOnChanges
  - @Input属性发生变化的时候会被调用
  - 非@Input属性改变不会调用ngOnChanges
- ngDoCheck
  - 每次发生变更检查就会被调用一次
  - 谁在负责触发变更呢？ （Zones，它拦截了所有回调，定时器，事件，Ajax
  - 不要在ngDoCheck里面做非常消耗性能的事



### 变更检测的两种策略

- Default：无论哪个组件发生了变化，从根组件开始全局遍历调用ngDoCheck（）
- OnPush：只有当组件的@Input属性发生变化的时候才会调用本组件的ngDoCheck()



### 动效

github.com/jiayihu/ng-animation



### 动态组件

4个经典问题：

- 如何创建动态组件的实例

```javascript
首先在html中用#标记元素
@ViewChild("dynamic",{read:ViewContainerRef})
dyncomp:ViewContainerRef;


```

![1583935663324](F:\my-code\my-blog\Blog\source\_posts\my-doc\angular\angular-damo\1583935663324.png)

![1583935718151](F:\my-code\my-blog\Blog\source\_posts\my-doc\angular\angular-damo\1583935718151.png)



- 如何 给动态组件传参数

```javascript
this.component1.instance.title = "test"
```



- 如何监听动态组件的事件

```javascript
this.component1.instance.onClick.subscribe();
```



- 如何销毁动态创建的组件实例

```javascript
this.comp1.instance.destroy();
```





### ShadowDom

官方会自动处理shadowdom，不需要自己来设置。

启用shadowdom:  ViewEncapsulation.Native：样式和html都在shadowdom中。

![1583936270598](F:\my-code\my-blog\Blog\source\_posts\my-doc\angular\angular-damo\1583936270598.png)



- ViewEncapsulation.Emulate   样式提取到head中了，但是angular加了后缀，html是shadowdom
- ViewEncapsulation.None 样式是全局的，不做任何处理，提取到head中



###  内容投影

其实就是vue中的插槽，react中的children

1. 组件中定义占位符

![1583937403580](F:\my-code\my-blog\Blog\source\_posts\my-doc\angular\angular-damo\1583937403580.png)

2. 使用占位符标签填坑

![1583937505593](F:\my-code\my-blog\Blog\source\_posts\my-doc\angular\angular-damo\1583937505593.png)



事件的处理：

![1583937652941](F:\my-code\my-blog\Blog\source\_posts\my-doc\angular\angular-damo\1583937652941.png)



### ViewChild和ContentChild

- 用@ContentChild操作投影的内容
- 用@ContentChildren批量操作多块投影内容
- 用@ViewChild操作视图子节点
- 用@ViewChildren批量操作多个视图子节点

![1583938692976](F:\my-code\my-blog\Blog\source\_posts\my-doc\angular\angular-damo\1583938692976.png)

![1583938215880](F:\my-code\my-blog\Blog\source\_posts\my-doc\angular\angular-damo\1583938215880.png)



组件中使用：

用@ContentChildren(组件名)

`children:QueryList<ChildTwoComponent> `注入进来

![1583938423389](F:\my-code\my-blog\Blog\source\_posts\my-doc\angular\angular-damo\1583938423389.png)





# 指令

为什么需要指令

比如div有很多attribute，实际在自己的组件上是不能用的。而这些attribute可以解决很多问题。。。所以指令和这些attribute一样。

- 组件与指令之间的关系
  - 继承

![1584079259181](F:\my-code\my-blog\Blog\source\_posts\my-doc\angular\angular-大漠\1584079259181.png)

![1584079313152](F:\my-code\my-blog\Blog\source\_posts\my-doc\angular\angular-大漠\1584079313152.png)

所以指令的功能，在组件上面也是可以用@HostListener的。只是不建议这样用



- Angular内置指令（37个）
- 指令的作用（属性型与结构型）
- 自定义属性型指令（@HostListener与@HostBinding）
- 自定义结构型指令
- 指令之间如何交互



# 模块

- Angular的模块是用来组织业务的
- 每个应用至少有一个根模块
- 每个组件必须属于一个模块，而且只能属于一个模块
- 模块是@angular/cli打包的最小单位
- 模块也是Router异步加载时的最小单位



# 路由

- 前端为什么需要路由
- 路由基本用法（同步路由与router-outlet)
  - 通配符在最后

![1584080232087](F:\my-code\my-blog\Blog\source\_posts\my-doc\angular\angular-大漠\1584080232087.png)

- 路由与懒加载模块

1. 根模块用Router.forRoot(routes)

![1584080508324](F:\my-code\my-blog\Blog\source\_posts\my-doc\angular\angular-大漠\1584080508324.png)

2. 子模块里面用`Router.Module.ForChild() `//子路由可以无限嵌套。

![1584080587580](F:\my-code\my-blog\Blog\source\_posts\my-doc\angular\angular-大漠\1584080587580.png)

- N层嵌套路由

```javascript
<route-outelet></route-outlet> //组件显示
```



- 共享模块

![1584081062545](F:\my-code\my-blog\Blog\source\_posts\my-doc\angular\angular-大漠\1584081062545.png)

- 监听路由事件

![1584081111666](F:\my-code\my-blog\Blog\source\_posts\my-doc\angular\angular-大漠\1584081111666.png)



获取当前路由的实例：

![1584081194121](F:\my-code\my-blog\Blog\source\_posts\my-doc\angular\angular-大漠\1584081194121.png)

- 
- 传递和获取路由参数（单个参数、矩阵式参数）

![1584081256842](F:\my-code\my-blog\Blog\source\_posts\my-doc\angular\angular-大漠\1584081256842.png)

- 用代码触发路由导航

![1584081604180](F:\my-code\my-blog\Blog\source\_posts\my-doc\angular\angular-大漠\1584081604180.png)

- 预加载策略

![1584081851982](F:\my-code\my-blog\Blog\source\_posts\my-doc\angular\angular-大漠\1584081851982.png)



### 高级用法

- 【加载策略 】如何预加载模块
- 【加载策略 】如何自定义预加载测略
- 【路由守卫】如何控制模块预加载
- 【路由守卫】如何控制非授权访问
- 【路由守卫】如何保护用户输入的内容不丢失
- 【辅助路由】同一个模板里面使用多个router-outlet?



# 表单

- 模板驱动型表单     模板里面做 ，加标记（required，）

![1584348714048](F:\my-code\my-blog\Blog\source\_posts\my-doc\angular\angular-大漠\1584348714048.png)

- 响应式表单 

用代码的方式，来写![1584348729167](F:\my-code\my-blog\Blog\source\_posts\my-doc\angular\angular-大漠\1584348729167.png)

![1584348759759](F:\my-code\my-blog\Blog\source\_posts\my-doc\angular\angular-大漠\1584348759759.png)



- 动态表单

![1584348768875](F:\my-code\my-blog\Blog\source\_posts\my-doc\angular\angular-大漠\1584348768875.png)

- 数据校验

![1584348892179](F:\my-code\my-blog\Blog\source\_posts\my-doc\angular\angular-大漠\1584348892179.png)





# RxJS

- Rx简介
- RxJS与Promise类比 
- RxJS VS Promise 三个最重要的点

![1584350448668](F:\my-code\my-blog\Blog\source\_posts\my-doc\angular\angular-大漠\1584350448668.png)

- Angular中RxJS典型场景1 ：Http服务 
- Angular中RxJS典型场景2：事件处理

- 工具
  - [rx可视化工具](<https://github.com/moroshko/rxviz>)
- 常用函数23个。使用频率最高的10个

![1584358303603](F:\my-code\my-blog\Blog\source\_posts\my-doc\angular\angular-大漠\1584358303603.png)