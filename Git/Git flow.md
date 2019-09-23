## git-flow 

git 最强大的就是其分支功能，但是如何分支才能更有效的提高开发效率，减少因为代码合并带来的问题，需要一个分支模型来规范，其实在 git flow 出现之前，已经有分支模型理论流程，当时是根据此理论，手动的按照规范操作分支，git flow 出现之后，将一部分操作流程简化为命令，并没有增加新的功能，只是简化了操作。

## 安装 

```shell
#Mac
# 稳定版
brew install git-flow-avh
# 开发版
brew install git-flow-avh --HEAD
```

## 命令

### 初始化项目

```shell

# 在你项目控制执行下面的命令，然后一直回车
git flow init -f
#或者 -d  就不用回车了

```

## 分支模型

git flow 初始化工程目录完成后，只能看到两个分支：

master 和 develop 这两个分支被称为**长期分支** ，存在于项目的整个生命周期中，其他分支，是临时性的，根据需要来创建，当完成了自己的任务后，就会被删掉。

### 长期分支

#### master

**master**: 用于保存的是随时可在生产环境中部署的代码的分支

用于上线的分支，保护性分支，只包含经过测试的稳定代码，开发人员不能直接工作在此分支上，也不能直接提交改动到 **master** 分支上。

#### develop

**develop**: 用于保存当前最新开发成果的分支.

是开发人员进行任何新的开发的基础分支，当开始一个新的 **feature** 分支的时候，要从 **develop** 分出去；

父分支为**master**.

当新功能代码完成后,可以发布**release**分支,用于测试.

### 辅助分支

#### feature 分支

**feature**: 用于开发各种新功能的分支.

每一个新功能的开发都应该各自使用独立的分支。每个 feature 分支颗粒要尽量小，以利于快速迭代和避免冲突,否则冲突解决起来就没完没了。

在创建新的功能开发分支时，父分支为 **develop**（而不是 master）。

当功能开发完成时，改动的代码要被合并到 **develop** 分支,然后删除该**feature**分支并切换**develop**分支。

功能开发永远不应该直接牵扯到 **master**。

##### feature 分支命令

```shell
#创建 feature 分支 
git flow feature start <branch-name>
#完成一个 feature 分支
git flow feature finish <branch-name>
#该命令会把我们在当前分支的代码整合到‘develop’分支中去，之后，git-flow 会进行清理操作，删除当下完成的功能分支，将分支切换到‘develop’。
```

#### release 分支

**release**:用于预发布测试的分支

一旦 **develop** 分支积聚了足够多的新功能（或者预定的发布日期临近了），可以基于 **develop** 分支建立一个用于产品发布的分支。

**release** 分支一旦建立就将独立，不可再从其他分支 pull 代码

**release**分支的创建意味着一个发布周期的开始 ,在这个分支上只能修复 bug，做一些文档工作或者跟发布相关的任务。

在一切准备就绪的时候，这个分支会被合并入 **master**，并且用版本号打上标签。另外，发布分支上的改动还会合并入 **develop** 分支

 在发布周期内，develop 分支仍然在被使用（可以把其他功能集成到 develop 分支）。

使用**release** 来为发布做准备的好处是，在一部分忙于当前的发布的同时，其他人可以继续为接下来的一次发布开发新功能。

##### release 分支命令

```shell
#创建 release 分支 ,release 分支是使用版本号命名的
git flow release start <branch-name>
#完成一个 release 分支
git flow release finish <branch-name>
#该命令会把我们在当前分支的代码整合到 master和 develop 分支中
#版本被打上 tag‘版本号’,删除本地’release,切换分支到 develop
```

#### hotfix 分支

**hotfix**:用于快速给已发布产品修复 bug 或微调功能的分支

发布后的维护工作或者紧急问题的快速修复也需要使用一个独立的分支。这是唯一一种可以直接基于 **master** 创建的分支。

一旦问题被修复了，所做的改动应该被合并入 **master** 和 **develop** 分支（或者用于当前发布的分支）。在这之后，**master** 上还要使用更新的版本号打好标签。

##### hotfix 分支命令

```shell
#创建 hotfix 分支 ,
git flow hotfix start <branch-name>
#完成一个 hotfix 分支
git flow hotfix finish <branch-name>

```

### 分支命名规范

| 分支    | 规范                               |
| ------- | ---------------------------------- |
| master  | 无                                 |
| develop | 无                                 |
| feature | 开发的模块名,类名,方法名,功能简述  |
| release | 版本号如:1.0/ V1.1 之类的          |
| hotfix  | bug 号,修复的方法名,解决的问题简述 |

### 分支之间的关系

![47176bf6-db8c-11e9-bad3-acde48001122](https://i.loli.net/2019/09/20/pexY2fMEOa5n7SR.png )