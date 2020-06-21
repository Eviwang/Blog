linux下 安装 centos 7



## 参考

推荐下面这篇文章：

https://www.jianshu.com/p/7e6ea273833d

没有响应的问题：

https://segmentfault.com/a/1190000017436142





## 安装虚拟机CentOS7

装好后可以 远程连接这台虚拟机

ssh root@10.110.16.12





## 准备

1. 关闭firwalld防火墙开机启动

   systemctl stop firewalld

   systemctl disable firewalld

2. 关闭SELINUX 并重启  （强制访问安全策略）

   `vi /etc/sysconfig/selinux`

   `SELINUX=disabled  //设置这里`

3. reboot  命令重启系统

最后：可以使用   `getenforce 查看是否关闭`



## 安装 Omnibus Gitlab-ce package 社区版本

Omnibus Gitlab-ce  一件安装包。而不是用源码安装

1. 安装Gitlab组件

   ```shell
   yum -y install curl policycoreutils openssh-server openssh-clients postfix
   ```

2. 配置yum 仓库

   ```shell
   curl -sS https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.rpm.sh  | sudu bash
   ```

3. 启动 postfix邮件服务

   ```shell
   systemctl start postfix
   systemctl enable postfix
   ```

4. 安装gitlab-ce社区版本

   `yum install -y gitlab-ce`



## Gitlab安装配置管理

1. 证书创建与配置加载
2. Nginx SSL代理服务设置
3. 初始化Gitlab相关服务并完成安装

```
mkdir -p /etc/gitlab/ssl
openssl genrsa -out "/etc/gitlab/ssl/gitlab.example.com.key 2048"
openssl req -new -key "/etc/gitlab/ssl/gitlab.example.com.key" -out "/etc/gitlab/ssl/gitlab.example.com.csr"
```

![1591976208925](F:\my-code\my-blog\Blog\source\_posts\my-doc\gitlab 环境搭建\gitlab环境搭建-images\1591976208925.png)

然后查看：

ll

创建签署证书：

```
openssl x509 -req -days 365 -in "/etc/gitlab/ssl/gitlab.example.com.csr" -signkey "/etc/gitlab/ssl/gitlab.example.com.key" -out "/etc/gitlab/ssl/gitlab.example.com.crt"
```

创建pem证书：

```
openssl dhparam -out /etc/gitlab/ssl/dhparams.pem 2048
```

然后查看：

ll

最终结果：

![1591976507337](F:\my-code\my-blog\Blog\source\_posts\my-doc\gitlab 环境搭建\gitlab环境搭建-images\1591976507337.png)

然后更改权限：

```
chomod 600 *
```



## 配置gitlab

vi /etc/gitlab/gitlab.rb



将

```nginx
# nginx["redirect_http_to_https"] = false//这行改为：
nginx["redirect_http_to_https"] = true

# nginx['ssl_certificate'] = "/etc/gitlab/ssl/#{node['fqdn']}.key"  //这行改为
nginx['ssl_certificate'] = "/etc/gitlab/ssl/gitlab.example.com.crt"
# nginx['ssl_certificate'] = "/etc/gitlab/ssl/#{node['fqdn']}.key"  //这行改为
nginx['ssl_certificate_key'] = "/etc/gitlab/ssl/gitlab.example.com.key"  

# nginx['ssl_dhparam'] = nill//这行改为：
nginx['ssl_dhparam'] = /etc/gitlab/ssl/dhparams.pem


```

保存。

输入命令，初始化配置:

```shell
gitlab-ctl reconfigure
```

## 更改nginx

```nginx
vi /var/opt/gitlab/nginx/conf/gitlab-http.com.conf


server_name gitlab.example.com//在它的下面添加一样
rewrite ^(.*)$ https://$host$1 permanent;
```

## 重启nginx

```
gitlab-ctl restart
```





## 更改windows host

`C:\Windows\System32\drivers\etc`

添加一行,将域名对应到主机ip：

10.110.16.20 gitlab.example.com



## 搞定：

浏览器输入：gitlab.example.com















## 遇到的问题：

1. 没网
2. ssh链接不上虚拟机
3. 虚拟机没有ip

[解决](https://www.cnblogs.com/shanghongyun/p/10179569.html)：

```
vi /etc/sysconfig/network-scripts/ifcfg-ens33
onboot=no//改为onboot=yes

reboot //重启 
```





