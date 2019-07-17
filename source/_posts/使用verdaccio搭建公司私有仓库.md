---
title: 使用verdaccio搭建公司私有仓库
date: 2019-07-17 15:58:07
tags:
---

## 安装

```javascript
npm install -g verdaccio
```

## 启动服务

```javascript
$> verdaccio
warn --- config file  - /home/.config/verdaccio/config.yaml
warn --- http address - http://localhost:4873/ - verdaccio/3.0.0
```

## 发布包

```javascript
npm adduser --registry http://localhost:4873
//输入注册账号名，可以在web端登录

npm publish --registry http://localhost:4873
```

## 删除包

删除需要找到安装目录的指定的文件夹，直接删除目录即可
```
C:\Users\evi.wang\AppData\Roaming\verdaccio\storage
```


## 参考链接
- https://verdaccio.org/
- https://blog.csdn.net/qq_29594393/article/details/81587989
- [用nrm一键切换npm源](https://www.cnblogs.com/wangmeijian/p/7072053.html)