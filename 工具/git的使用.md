# @`Git`

待编辑...

## 查看远程分支

```
git branch -a
```

## 删除远程分支

```shell
# 删除远程分支
git push origin --delete <branchName>

# 推送空分支到远程 也可以删除远程分支
git push origin :<branchName>

# 删除tag
git push origin --delete tag <tagname>
git tag -d <tagname>
git push origin :refs/tags/<tagname>
```

## 删除不存在对应远程分支的本地分支

```shell
# 开发者A 创建本地分支 origin/bugfixA1 推送到远程分支
# 开发者B fetch或者pull在本地更新了分支 origin/bugfixA1
# 开发者A bug修复完 删除origin/bugfixA1 推送到远程分支
# 开发者B 再次fetch或者pull 并不会删除本地分支originbugfixA1 git branch -a 也不会看到删除状态

git remote show origin // 查看所有origin状态  被删除分支被标记为  stale 状态

git remote prune origin //删除本地 stale 状态的分支
```

## 修改远程地址

```
 git remote set-url origin 新地址
```

# @ 参考

[Git: Delete a branch (local or remote)](https://makandracards.com/makandra/621-git-delete-a-branch-local-or-remote)
[How do I delete a Git branch both locally and remotely?](https://stackoverflow.com/questions/2003505/how-do-i-delete-a-git-branch-both-locally-and-remotely)
