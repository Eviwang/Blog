安装docker

https://imroc.io/posts/docker/quick-start-for-docker-3/

```
# step 1: 安装必要的一些系统工具
sudo yum install -y yum-utils device-mapper-persistent-data lvm2
# Step 2: 添加软件源信息
sudo yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
# Step 3: 更新并安装 Docker-CE
sudo yum makecache fast
sudo yum -y install docker-ce
# Step 4: 开启Docker服务
sudo service docker start
```









刚在新的Centos上安装Docker-CE,后运行`docker run hello-world`报错`Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?`

解决办法


```bash
$ systemctl daemon-reload
$ sudo service docker restart
$ sudo service docker status (should see active (running))
$ sudo docker run hello-world`
```





下载 [winSCP](<https://winscp.net/eng/download.php>) 文件服务器





中断下载：

```
ctrl + z
ps -ef | grep yum
kill -9 pid
```



## 镜像

```bash
https://dockerhub.azk8s.cn/
```

```
1.修改或创建daemon.json文件：vi /etc/docker/daemon.json
 
将以下配置写入到文件中，保存并退出（不会操作的百度下vi命令吧）：
 
{
 
"registry-mirrors": ["http://hub-mirror.c.163.com"]
 
}
 
2.重启docker：systemctl restart docker.service
```







##  退出node环境

```bash
> .exit

```





找不到docker

<https://blog.csdn.net/textdemo123/article/details/97116499>







## 常见问题

错误：

```bash
error during connect: Get http://docker:2375/v1.40/containers/json?all=1: dial tcp: lookup docker on 67.207.67.2:53: no such host
```



解决思路：

1. 在`/etc/gitlab-runner/config.toml`配置文件下确保 `privileged = true`     [参考](https://devops.stackexchange.com/a/9446)

2. 查看状态：

   ```
   gitlab-runner status
   
   systemctl is-enabled gitlab-runner  //意思是是否开机启动
   
   systemctl is-enabled docker  //意思是是否开机启动
   ```

3. 设为开机启动

   ```bash
   systemctl enable docker
   //  参考：https://zhuanlan.zhihu.com/p/97117678
   ```

   