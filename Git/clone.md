遇到了这个情况，当前本地的文件已经改的面目全非，但还没`push`到远程；我想恢复到上一次提交

```bash
# 
git status  # 查看所修改的文件
git restore <file> # 方法一

git reset --hard HEAD #方法二
# 其他暂且不表
```

那如果重新`clone`仓库，但是我只需要克隆仓库的子文件夹

```bash
git clone 仓库地址 
# 无法直接克隆远程仓库的单个子文件或子目录
# 稀疏检出 Sparse Checkout 先留个引子
```

