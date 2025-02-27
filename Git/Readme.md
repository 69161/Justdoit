#### Git is a distributed version control system

#### Git is free software

#### Git 分布式版本控制系统

安装完成后，命令行设置

```
git config --global user.name "your name"
git config --global user.email "email@example.com"
```

设置参数后，表示这台机器上所有的Git仓库都会使用这个配置

创建版本库 （repository）仓库里面的所有文件都可以被Git管理起来，每个文件的修改、删除，Git都能跟踪，以便任何时刻都可以追踪历史，或者在将来某个时刻可以“还原”。

```
mkdir foldername
cd foldername
pwd //显示当前目录

git init //把这个目录变成Git可以管理的仓库

code . //windows下使用vscode打开当前文件夹

git add Readme.md

git commit -m "wrote a readme file about Git knowledge"  
//git commit -m 后面输入本次提交的说明

git status //时刻掌握仓库当前状态
git diff //查看不同
```

#### 版本回退

```
git log //历史记录  --pretty=oneline 
// commit id 
// HEAD 表示当前版本，HEAD^ 上一个版本 HEAD^^ 上上一个版本 HEAD~100 上100个版本
git reset --hard HEAD^ 
//--hard会回退到上个版本的已提交状态，而--soft会回退到上个版本的未提交状态，--mixed会回退到上个版本已添加但未提交的状态

git reset --hard "commit id 一般前4-5位"
```

#### 工作区与暂存区

工作区当前目录，工作区内一隐藏目录`.git`是Git的版本库；

版本库里存的很多东西，最重要的是暂存区（stage），还有Git为我们自动创建的第一个分支`master`，以及指向`master`的一个指针叫`HEAD`。

![git-repo](https://liaoxuefeng.com/books/git/time-travel/working-stage/repo.png)

```
git add //将工作区文件提交到暂存区
git commit //暂存区的所有内容提交到当前分支
//提交后又没对工作区做任何修改，那工作区就是干净的
$ git status
On branch master
nothing to commit, working tree clean
//暂存区就没有任何内容了
```

![git-stage-after-commit](https://liaoxuefeng.com/books/git/time-travel/working-stage/commit.png)

