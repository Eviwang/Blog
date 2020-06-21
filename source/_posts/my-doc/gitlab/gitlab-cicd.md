[文档](<https://docs.gitlab.com/ee/ci/>)

配置CICD事件触发：

`settings` -> `webhook `



## 安装gitlab-runner



安装的几种方式：

- [手动档](https://docs.gitlab.com/runner/install/linux-manually.html#using-binary-file)
- [脚本自动挡](https://docs.gitlab.com/runner/install/linux-repository.html)

遇到问题，curl is unable to connect to packagecloud.io over TLS ，解决：

```
systemctl enable sshd
systemctl start sshd 
```



## 使用注册runner

https://docs.gitlab.com/runner/register/index.html







## 怎么使用scp做部署

https://stackoverflow.com/a/43629736

1. 生成秘钥

   ```
   ssh-keygen -t rsa //生成公钥和私钥
   回车输入ci会生成两个文件：
   ci ci.pub
   ```

2. 将私钥存到 gitlab ci 里面：settings-> ci/cd -> Variables 

   ​	- `SSH_PRIVATE_KEY`

3. 将公钥添加到服务器的`~/.ssh/authorized_keys`文件中

4. 将脚本放到 `before_script`

   ```
   - 'which ssh-agent || ( apt-get update -y && apt-get install openssh-client -y )'
   # Run ssh-agent (inside the build environment)
   - eval $(ssh-agent -s)
   # Add the SSH key stored in SSH_PRIVATE_KEY variable to the agent store
   - ssh-add <(echo "$SSH_PRIVATE_KEY")
   - mkdir -p ~/.ssh
   - '[[ -f /.dockerenv ]] && echo -e "Host *\n\tStrictHostKeyChecking no\n\n" > ~/.ssh/config'
   ```



.gitlab-ci.yml:

```
image: node:10

stages:
  - deploy

before_script:
  - 'which ssh-agent || ( apt-get update -y && apt-get install openssh-client -y )'
  # Run ssh-agent (inside the build environment)
  - eval $(ssh-agent -s)
  # Add the SSH key stored in SSH_PRIVATE_KEY variable to the agent store
  - ssh-add <(echo "$SSH_PRIVATE_KEY")
  - mkdir -p ~/.ssh
  - '[[ -f /.dockerenv ]] && echo -e "Host *\n\tStrictHostKeyChecking no\n\n" > ~/.ssh/config'

step-deploy-prod:
  stage: deploy
  tags:
    - linux
  script:
    - scp index.js root@192.168.88.128:~/

```





## 安装nginx

https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-centos-7

nginx端口被占用：

https://blog.csdn.net/qq_40907977/article/details/91989353



## 参考

