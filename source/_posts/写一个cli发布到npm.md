---
title: 写一个cli发布到npm
date: 2019-07-02 13:27:52
tags: [npm,cli]
---

## `npm init -y` 初始化配置

在`package.json`中配置版本号，和包的名字

## 新建`index.js`文件

<!-- more -->
```javascript
// 这里表示默认使用 node 打开
#!/usr/bin/env node
console.log("hello world!");
```

## 在package下面加入节点

新建一个index为入口文件
```javascript
    {
    "bin": {
        "hello-cli": "index.js"//这个是命令名字,到时候会执行index.js
    }
}
```

## 本地使用

`npm link`这个会将`hello-cli`命令加入到
`C:\Users\evi.wang\AppData\Roaming\npm`

可以使用
`hello-cli`跑起来了

## 发布到npm

1. https://www.npmjs.com 注册帐号
2. 创建自己的项目
3. 运行 `npm adduser`
4. 执行`npm publish`
5. 在`npm.js`网站上搜索包名。

## Q&A

1. `publish Failed PUT 403` 说明没有权限，需要换一个名字。或者版本号有问题

## 参考

- https://juejin.im/post/5bd90d3ce51d4579362b0390
- http://test.imweb.io/topic/59ffc48c1f0e50753869bf91