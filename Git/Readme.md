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

##### 版本回退

```
git log //历史记录  --pretty=oneline 
// commit id 
// HEAD 表示当前版本，HEAD^ 上一个版本 HEAD^^ 上上一个版本 HEAD~100 上100个版本
git reset --hard HEAD^ 
//--hard会回退到上个版本的已提交状态，而--soft会回退到上个版本的未提交状态，--mixed会回退到上个版本已添加但未提交的状态

git reset --hard "commit id 一般前4-5位"
```

##### 工作区与暂存区

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

##### 管理修改

简单的说，Git追踪的是管理修改并非文件，工作区修改后内容`add`后存入暂存区（stage）`commit`后提交到分支

##### 撤销修改

```
git restore file  //把file在工作区的修改全部撤销
// 一种是file 自修改后还没有被放到暂存区，撤销修改就回到和版本库一模一样的状态
// 一种是file 已经添加到暂存区后，又作了修改，撤销修改就回到添加到暂存区后的状态
// 让file 回到最近一次git commit或git add时的状态
git restore . //丢弃所有未暂存的修改 慎用！
```

```
git restore --staged <file> 
// 将文件从暂存区移出，但保留工作目录中的更改
// 若不加--staged 会直接丢弃工作目录中未暂存的修改，将其恢复到最近一次提交的状态
```

##### 删除文件

```
git rm
```

#### 远程仓库

以GitHub为例

1. 创建SSH Key，先看主目录下（/c/Users/xxx)下是否有`.ssh`文件夹，看下文件内是否有`id_rsa`和`id_rsa.pub`若没有可创建

```
ssh-keygen -t rsa -C "youreEmail@example.com"
```

​	然后一路回车，创建成功后`.ssh`文件夹下有`id_rsa`(私钥）和`id_rsa.pub`（公钥）

2. 登录Github，`Settings=>SSH and GPG keys=>new SSH Key` 填写上你的`id_rsa.pub`内容，然后保存
3. 添加远程库（repository）
4. 本地工作台与远程库建立关联	

```
git remote add origin https://github.com/69161/Justdoit.git
// remote 远程 添加 origin 原来的 起源
git branch -M main
// -m 重命名分支
git push -u origin main // 第一次推送  -u
git push origin main // 之后每次推送
```

5. 删除远程库

   ```
   git remote -v //查看远程库信息
   git remote rm origin //"删除"本质是解除了本地与远程的绑定关系
   ```

6. 远程库克隆

   ```
   git clone git@github.com:69161/Justdoit.git
   ```

#### 分支管理

1. 创建与合并分支

   如今只有一条分支`main`；在版本回退中，`HEAD`指向`main`；

   每次提交，`main`分支向前移动一步

   创建新的分支 `dev` 指向与`main`相同的提交，再把`HEAD`指向`dev`表示当前分支在`dev`上

   之后每次提交`dev`向前一步，`main`指针不变（如下图，把`master`改为`main`理解）

   [![3dRCKQ9.md.png](https://iili.io/3dRCKQ9.md.png)](https://freeimage.host/i/3dRCKQ9)

​	`dev`工作完成，合并到`main`上，直接把`main`指向`dev`的当前提交，就完成了合并

​	![3dRxSuR.png](https://iili.io/3dRxSuR.png)

​	然后删除`dev`分支

```
git switch -c <新分支> //创建并切换分支
git switch <分支> //切换分支
git checkout <分支> //切换分支

git branch //查看本地分支，带*为当前分支
git branch -a //查看所有分支（含远程）
git branch <分支名> //创建分支
git branch -d <分支名> //删除分支
git branch -D <分支名> //强制删除分支
git branch -m <新分支名> //重命名分支
```

合并分支

```
//在 dev 分支上git add git commit 后
git switch main //切换回main分支
git merge dev //将dev分支合并到当前分支
git branch -d dev //删除dev分支
```

2. 解决合并分支冲突

```
git switch -c feature
git add 
git commit
git switch main
git add
git commit
git merge feature //提示冲突 <<< === >>> 根据需求更改后再add commit
git add 
git commit
git branch -d feature
```

![3dRxvyv.png](https://iili.io/3dRxvyv.png)

3. 通常合并分支用`Fast forward`模式，但删除分支后会丢掉分支信息

   强制禁用`Fast forward`  `--no-ff` git会再`merge`时生成一个新的`commit`

   ```
   git switch -c dev
   git add
   git commit
   git switch main
   git merge --no-ff -m "merge with no-ff" dev // 生成新的commit -m 描述
   ```

   ```
   git log --graph --pretty=oneline --abbrev-commit // 查看分支历史
   git log --oneline --graph
   ```
   
   ###### 分支策略
   
   `main`分支是非常稳定的，仅用来发布新版本；比如1.0版本发布，再把`dev`合并到`main`上发布
   
   `dev`是小伙伴干活的地方，每个人都有自己的分支，时不时的合并到`dev`上
   
   ![git-br-policy](https://liaoxuefeng.com/books/git/branch/policy/branches.png)

4. bug分支

   ```
   git status // 查看工作台的状态，当前工作未完成无法提交
   git stash // 把当前工作台储存起来
   
   // 在main分支上处理bug
   git switch main
   git switch -c issue-100
   git add
   git commit 
   git switch main
   git merge --no-ff -m "merge bug fix 100"
   git branch -d issue-100
   
   git switch dev //切回dev分支工作
   
   git stash list //看到之前储存的工作现场
   git stash apply //恢复 但是 stash 内容不删除，需要 git stash drop 删除
   git stash pop //恢复的同时把stash也删除
   git stash apply stash@{0} // 恢复指定的stash
   ```

   `main`分支上修复了bug，`dev`早期从`master`分支出来的，bug也存在于`dev`上

   简单的修复，只需要把bug提交所做的修改“复制”到`dev`分支

   ```
   git branch //确定已切换到dev分支上
   git cherry-pick <bug提交的commit>
   ```

5. feature 分支

   开发新功能

   情况变动，新功能删除 `git branch -D feature`

   

   
