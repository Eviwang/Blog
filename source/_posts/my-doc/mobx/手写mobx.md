## Object.defineProperty

1. 不支持数组
2. 不支持新增属性

##  Proxy & Reflect

被代理的数组变化时，会触发两次change，

- 第一个元素的改变
- length 的改变 



## Decorator

### 装饰类参数

```javascript
@test
class Person{
    
}
function test(Person)
```



### 装饰属性参数

```javascript

class Person{
    @readonly PI = 3
}
//参数
function readonly(Person.prototype,propName,descriptor){
    // 这里descriptor有个方法，调用后会返回默认值3。descriptor.initializer
}
```



### 装饰类里面的方法参数

```javascript
class Person{
    @log
    methed(){
        
    }
}
//参数
function log(Person.prototype,propName,descriptor){
    // 这里的descriptor.value就是那个method函数
}
```





## Observer的简单实现

对 `componentWillMount `生命周期函数进行拦截：

```javascript

const instance = target.prototype;
const cwm = instance.componentWillMount;
instance.componentWillMount = function () {
    cwm && cwm.call(this);
    autorun(() => {
        this.render();
        this.forceUpdate();
    });
};
```

