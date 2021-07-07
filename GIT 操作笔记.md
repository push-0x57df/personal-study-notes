# Git 操作笔记

## 添加用户名和邮箱

Git是一个多用户的版本控制工具，每个用户必须输入用户名和邮箱

``` powershell
git config --global user.email "<邮箱>"
git config --global user.name "<用户名>"
```

## 生成ssh秘钥

``` powershell
ssh-keygen -t rsa -C "<邮箱>" -f c:\\ssh\.ssh
```

加上-f参数是生成路径

## 新建本地仓库

使用Git前，需要先创建一个本地仓库，可以使用一个已经存在的目录作为仓库。

使用当前目录作为本地仓库，只需要初始化：

``` powershell
git init
```

使用我们指定目录作为Git仓库:

``` powershell
git init <新目录完整名称>
```

## 添加新文件到暂存区

使用命令将制定文件提交到暂存区：

``` powershell
git add <目录或文件的完整名称>
```

使用命令将本地库中所有的文件添加到暂存区

``` powershell
git add .
```

## 查看Git状态信息

``` powershell
git status
```

## 查看全部分支信息

``` powershell
git branch --all
```

## 提交版本

将暂存区文件提交到本地库

``` powershell
git commit -m "<注释信息>"
```

不使用-m，编辑器会提示键入注释信息

可以使用 **-a** 标识避免每次提交都要添加缓存区（add命令）

``` powershell
git commit -a -m "<注释信息>"
```

## 查看文件状态

使用命令

``` powershell
git status -s
```

## 查看已配置的远程仓库

``` powershell
git remote
```

## 配置远程仓库

注意：配置仓库之前请生成 ssh 秘钥，并把公钥配置到 Git 服务器上

``` powershell
git remote add <远程仓库名称> <远程仓库地址-ssh地址>
```

## 移动远程仓库 HEAD

``` powershell
git remote set-head origin develop
```

## 回退版本

1. 查询日志，找到想回退的提交号

   ``` shell
   git log
   ```

2. 回退版本

   ``` shell
   git reset --hard 45ba7d3b95458fe5642618bbf85ac018ba2246f1
   ```

3. 强制提交

   ``` shell
   git push -f
   ```

## 发布版本

1. 语法

   ``` powershell
   git push <远程主机名> <本地分支名>:<refs/for/远程分支名>
   ```
   
2. 如果当前分支与远程分支存在追踪关系，则本地分支和远程分支都可以省略，将当前分支推送到origin主机的对应分支

   ``` powershell
   git push <远程主机名>
   ```

3. 如果远程分支被省略，如上则表示将本地分支推送到与之存在追踪关系的远程分支（通常两者同名），如果该远程分支不存在，则会被新建

   ``` powershell
   git push <远程主机名> <本地分支名>
   ```

4. 如果省略本地分支名，则表示删除指定的远程分支，因为这等同于推送一个空的本地分支到远程分支，等同于 git push origin --delete master

   ``` powershell
   git push <远程主机名> :<refs/for/远程分支名>
   ```

5. 如果当前分支只有一个远程分支，那么主机名都可以省略，形如 git push，可以使用git branch -r ，查看远程的分支名

   ```powershell
   git push
   ```

6. 关于 refs/for

   refs/for 的意义在于我们提交代码到服务器之后是需要经过code review（代码审查）之后才能进行merge（合并）的，而refs/heads 不需要

## 创建分支

创建一个分支并切换上去，创建是基于当前分支的

``` powershell
git checkout -b <分支名称>
```

这条指令分开写为：

``` powershell
git branch <分支名称>
git checkout <分支名称>
```

## 切换分支

``` powershell
git checkout <分支名称>
```

## 合并分支

假如我们现在在dev分支上，刚开发完项目，执行了下列命令：

``` powershell
git  add .
git  commit -m ' <提交的备注信息>'
git  push origin dev
```

想将dev分支合并到master分支，操作如下：

1. 首先切换到master分支上

   ``` powershell
   git checkout master
   ```

2. 如果是多人开发的话 需要把远程master上的代码pull下来

   ``` powershell
   git pull <远程主机名> master
   ```

3. 然后我们把dev分支的代码合并到master上

   ``` powershell
   git merge dev
   ```

4. 然后查看状态及执行提交命令

   ``` powershell
   git status
   
   On branch master
   Your branch is ahead of 'origin/master' by 12 commits.
     (use "git push" to publish your local commits)
   nothing to commit, working tree clean
   
   #上面的意思就是你有12个commit，需要push到远程master上 
   #最后执行下面提交命令
   git push <主机名> master
   ```

## 删除分支

如果我们已经将临时工作分支合并到了主工作分支上（开发分支或者主分支），临时分支已经不再需要时，想要删除临时分支

``` powershell
git branch -d <要删除的分支名称>
```

## 查看Git日志

``` powershell
git log
```

## 克隆Git仓库以加入工作

``` powershell
git clone <git地址>
```

如果需要克隆的不是 master 分支，需要克隆 develop 分支：

``` powershell
git clone -b develop <git地址>
```

## 修改 ssh 秘钥位置

如果因为某些原因 ssh秘钥不能放在默认的位置，需要修改 git 配置中有关秘钥位置的设置

例如秘钥在 D:/ssh

需要将私钥位置写入配置文件

``` powershell
git config --global core.sshCommand "ssh -i d:/ssh/id_rsa"
```

## 修改配置

``` powershell
//查
git config --global --list
 
git config --global user.name
 
//增
git config  --global --add user.name jianan
 
//删
git config  --global --unset user.name
 
//改
git config --global user.name jianan
```

## 案例一：第一次提交项目源码

``` powershell
#本案例建立在已经配置好Git用户名和邮箱的前提下，服务器端已经部署客户端的ssh公钥
#初始化本地仓库
git init
#提交全部文件进入暂存区
git add .
#提交版本
git commit -m "启用Git托管的首次提交"
#配置远程仓库，origin是仓库名称，也可以是其他名称，但在下面的操作中需要使用刚刚配置的远程仓库名称
git remote add  <远程仓库ssh地址>
#第一次推送代码到远程仓库，后续推送只要使用git push
git push --set-upstream origin master
```
