# [**推荐知乎的这篇文章**](<https://zhuanlan.zhihu.com/p/98679880>)

# Git

###  最小配置

1. 配置用户名邮箱

```bash
git config --global user.name ‘your_name’
git config --global user.email ‘your_email@domain.com’
```

2. config 的三个作⽤用域

```bash
$ git config --local  // 当前仓库
$ git config --global // 当前登录用户
$ git config --system // 不常用，对系统所有用户
```

3. 显示

```bash
$ git config --list --local
$ git config --list --global
$ git config --list --system
```

4. 设置与清除

```bash
git config --global user.name ‘your_name’

$ git config --unset --local user.name
```



5. 优先级

local > global > system



### 建Git仓库

```bash
git init
git init you_project
```



### 命令

```bash
git mv readme readme.md //重命名

git log
git log --oneline //一行展示，展示4条
git log -n4 //展示4条
git log --all --graph //图形化展示，展示所有分支
git branch -v //查看本地分支

```

###  工具

-  gitk

```bash
gitk //打开图形界面

```

view菜单-> new View -> 勾选显示all branch



### .git 目录有什么

```bash
git cat-file -t  [hash]//查看 文件的类型
git cat-file -p  [hash]//查看 文件的内容
```



- HEAD文件

存的就是当前分支

- config
- refs文件夹
  - head 里面存放的是分支的commit的当前hash
  - tags
- objects
  - git cat-file -t  文件夹名[hash] //会展示tree

常见的git几种类型：

- commit
- tree //文件夹
- blob //文件

### commit,blob,tree三者关系

![1584427629170](F:\my-code\my-blog\Blog\source\_posts\my-doc\git三剑客\git三剑客\1584427629170.png)

在git中，只要文件相同，那么就是一个blob

查看提交中的信息：![1584428231517](F:\my-code\my-blog\Blog\source\_posts\my-doc\git三剑客\git三剑客\1584428231517.png)



### 分离头指针(detach HEAD)情况

分离头指针指的是： 直接 `git checkout 【hash】`

而没有和branch挂钩，会导致代码丢失



### HEAD和branch的关系

```bash
git checkout  -b test master //基于master分支创建test分支。
```

- 新建分支默认是和HEAD挂钩的
- 但是HEAD不一定是指向branch
  - HEAD
  - HEAD^^ // 第二种：父亲的父亲
  - HEAD~2 // 第三种，父亲的父亲



# Git常用场景

#### 分支操作

- 删除
  - git branch -d test
  - git branch -D test  强制删除
- 新建
  - git chekcout -b test
  - git chekcout -b test master  基于master创建分支



#### commit 操作

- 修改上一次commit message
  - `git commit --amend`



#### diff操作

![img](https://pic2.zhimg.com/80/v2-e95ac3baeb28734107f8bec468525661_720w.jpg)

- 暂存区和版本库比较

  ```bash
  git  diff --cached
  ```

- 工作区和暂存区差异比较

  ```bash
  git diff
  git diff -- readme.md // 比较单个文件
  ```

- 工作区和版本库比较

  ```
  git diff HEAD
  ```

  

其他：

- 比较两个分支

  ```bash
  git diff feauture/evi.wang master -- index.html //比较单个文件
  git diff feauture/evi.wang master
  ```

- 比较两个commit

  ```bash
  git diff hash1 hash2
  ```

  

#### 撤销操作

- revert

  将hash的那次commit的所有内容，反转过来。会丢弃

- reset

  - --hard

    全部丢弃，直接指向hash

  - --soft

    全部保存到暂存区，并且工作区的内容也不会丢掉

  - --mixed(默认)

    全部退回commit内容，并放到工作区

- 暂存区退回到工作区

  ```bash
  git reset HEAD  // 将暂存区更改全部拿到工作区
  git reset -- index.html // 撤销的单个
  ```

- 撤销工作区 

  原理就是用暂存区的内容，来覆盖工作区的内容

  ```bash
  git checkout -- index.html //  撤销单个
  git checkout .  //撤销所有
  ```

  


tips:

- 变更暂存区用 reset
- 变更工作区用 checkout
- revert 必须加hash，直接退到哪个版本，而且需要解决冲突



#### 临时暂存操作

```bash
git stash
git stash list
git stash apply 弹出，但还是保留栈里面的信息
git stash pop


```

#### 备份

- 哑协议 /user/beer.git   没有协议的，只有路径
- 智能协议  file:/user/code/beer.git

```bash
// 智能协议：
git clone --bare file://F:\my-code\git\git-jike\one-test\.git one.git//意思是生成.git备份文件

--bare 表示不带工作区

```

#### 本地搭建仓库中心：

1. 建立.git 备份文件中心。使用file协议

```bash
git clone --bare file://F:\my-code\git\git-jike\one-test\.git one.git
```

2. 用户A在备份中心拉代码。

```bash
git clone file://F:\my-code\git\git-jike\one-test\one.git
git remote add one file://F:\my-code\git\git-jike\one-test\one.git
```

3. 用户B同样，在备份中心拉代码。设置remote。

# GitHub

### 禁止条例：

- 禁止 `git push -f`
- 禁止在集成分支执行变更历史的操作  就是rebase

### GitHub为什么这么火

解决的用户的痛点

[features](<https://github.com/features>)

- code  review
- project manager
- integrations
- team managemeng
- Social coding
- document
- code hosting

[marketplace](<https://github.com/marketplace>)



### 怎样找到感兴趣的仓库

默认搜索是名称和描述

[高级搜索](<https://github.com/search/advanced>)

`react in:readme  //只搜索reamde中包含react的` 

 

### 搭建博客



### 如何保证开源质量

CI/CD

### 如何创建组织

profile -> Organizations -> New Organization

- 组织

- 团队
  - 不同的仓库分给不同的团队
  - 可以管理成员，分配权限

- 成员
  - 可以看到所有仓库，对于感兴趣的，可以发起申请

### 如何创建团队项目

1. New Repository -> 选择组织 

2. settings ->  Collaborators & teams 配置 团队和成员

### 怎样选择合适的团队工作流

- 主干开发

![1584510978403](F:\my-code\my-blog\Blog\source\_posts\my-doc\git三剑客\git三剑客\1584510978403.png)

- Git Flow

![1584510988671](F:\my-code\my-blog\Blog\source\_posts\my-doc\git三剑客\git三剑客\1584510988671.png)

- GitHub Flow

![1584511008247](F:\my-code\my-blog\Blog\source\_posts\my-doc\git三剑客\git三剑客\1584511008247.png)

- GitLab Flow

![1584511016954](F:\my-code\my-blog\Blog\source\_posts\my-doc\git三剑客\git三剑客\1584511016954.png)

- GitLab Flow(带环境分支)

![1584511042035](F:\my-code\my-blog\Blog\source\_posts\my-doc\git三剑客\git三剑客\1584511042035.png)

- GitLab Flow（带发布分支）

![1584511060639](F:\my-code\my-blog\Blog\source\_posts\my-doc\git三剑客\git三剑客\1584511060639.png)

### 如何挑选合适的分支集成策略

在Repository中选择Settings -> Network，可以看最近的分支图

Merge Button的三种策略：

- Allow merge commits

  产生一个merge commit合并到master

![1584513042258](F:\my-code\my-blog\Blog\source\_posts\my-doc\git三剑客\git三剑客\1584513042258.png)

- Allow squash merging

  把分支中的所有commit挑选出来直接在master提交。在master创建一个commit形成线性.没有箭头关联

  ![1584513251526](F:\my-code\my-blog\Blog\source\_posts\my-doc\git三剑客\git三剑客\1584513251526.png)

- Allow  rebase merging

  将分支中的所有commit原封不动的拿到master分支，形成线性

  ![1584513443810](F:\my-code\my-blog\Blog\source\_posts\my-doc\git三剑客\git三剑客\1584513443810.png)



### Issue

- label
- milestones
- issues  在settings-> Features-> Issues 里面可以配置模板

Issue模板会存放在`.github`的文件夹下面



### Project 项目管理面板

【project】 ->【创建】

三种模板：

- None    全部是自己建列
- Basic kanban  三种类型：Todo In Progress Done
- Automated kanban  跟Issue挂钩，自动转移状态
- Automated kanban with Review  和issue挂钩 并review
- Bug triage 

### Code Reivew

【Settings】-> 【Branches】 -> 【Branch 保护】-> 添加规则

必须review，必须要几个人review。都是可以设置的



### 团队写作如何做分支集成

```bash
git push -f origin 6ac0f:Shanghai //强制推送Shanghai的这个分支6ac0f这个commit 到远端
```



### 怎样保证集成的质量？

【Settings】-> 【Branches】 -> 【Branch 保护】-> 添加规则

添加 ci 集成，必须ci跑通，比如代码覆盖率。



### 怎样把产品包发布到GitHub上 【releases]

配置travis.yml达到下面的效果

- 自动code coverage
- 只要合并到master分支就发布版本
- 使用travis ci 变量来保护token

![1584620770095](F:\my-code\my-blog\Blog\source\_posts\my-doc\git三剑客\git三剑客\1584620770095.png)

###  如何写文档

wiki 本身 是一个git仓库，可以直接拉别人的写的好的wiki进行编辑

1. clone 别人的wiki 的git地址

2. 添加自己的origin，并拉代码

   `git add origin mywiki xxx.git`

3. 直接推到自己的wiki上面  

   `git push -f mywiki master`



# GitLab

提供了整个软件开发生命周期的工具

[devops](<https://about.gitlab.com/devops-tools/>)

- manage
- plan
- create
- verify
- package
- release
- configure
- monitor
- secure



github 叫 pull request

gitlab 叫 merge request



## gitlab 如何团队管理

## gitlab 如何code review

【settings】 -> Repository -> 【Protected Branch】



## CI/CD

【settings】 ->【CI/CD】 -> 【Runners】



## [gitlab 源码](<https://gitlab.com/gitlab-org>)和配置文件参考

