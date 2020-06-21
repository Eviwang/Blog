## Typescript基础



## 项目构建

创建项目

```shell
git clone https://github.com/alexjoverm/typescript-library-starter.git ts-axios
```





## 基础功能实现

对于有数组 和值对象，要处理的情况，统一转为 数组。



get 请求时，参数值为下面的情况：

- 数组
- 对象
- Date
- 特殊字符 `@:$,[]空格`
- 空值忽略
- 哈希忽略
- 已经存在的参数

post请求时：

- post对象转为JSON.stringify并且Content-Type为`application/json不然`服务端接受不到
- post ArrayBuffer

tips:

- 当post URLSearchParams或者FormData时，浏览器会自动帮我们加上 `Content-Type:application/x-www-form-urlencoded;charset=UTF-8`。<u>所以只有是纯对象的情况，才需要添加 `Content-Type为`application/json`</u>





服务端响应数据







## 异常情况处理

- 超时 `ontimeout`
- 



## 接口扩展



## 拦截器实现





## 配置化实现



## 取消功能实现



## 其他功能



## 单元测试



## 部署发布



