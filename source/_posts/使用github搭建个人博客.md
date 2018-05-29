---
title: 使用Github搭建个人博客
date: 2018-05-18 09:48:20
tags: Hexo
categories: Hexo
---

1. 在github 创建一个 仓库 比如`Eviwang.github.io`
2. 选择设置 找到  GitHub Pages  配置自己在阿里云购买的域名 blog.jerry-wang.cn。这里实际上会在GitHub仓库中创建一个CNAME的文件。
3. 选择一个主题，在仓库中添加  index.html 就是自己的网站了，此时就可以访问 `http://Eviwang.github.io`
4. 在阿里云域名管理中添加解析
5. 使用 hexo 发布到该仓库就可以了

tips:
```yml
# 刷新本地dns
ipconfig /flushdns 
```
