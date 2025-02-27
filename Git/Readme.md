#### Git is a version control system

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

