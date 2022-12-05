注意的地方：

1. 有新api的话需要red team view， 这个得在上线前做完: 参考https://issues.teslamotors.com/browse/CNDE-6190
2. 提pr至少需要两个approver.并且要让美国人approve
3. 每天记得log时间
4. 记得及时更新ticket状态
-------------------------------
## Ticket 工作流程
- 1. 通过Jira ticket 创建 git branch 



# Git

> 对比 2个分支 file 
git diff branch1  branch2 -- file 

git log <file> # 查看提交记录

## 提pr 流程
- 1.创建自己的开发分支（非必须）
git checkout -b CNDE-6916-vehicle-checkin-inspection-status

- 2. 实现需求或修改code
  vim ...
  git add <file> <file> 
  git add filename 
  git commit -m 'CNDE-xxxx : Descriptions' 
- 3. 修改完自测
自测完成，先不要提交pr,避免有其他人提交有更新的版本 先做一下同步
git rebase 和git merge的区别是 git rebase 形成的是一条线，会把你当前的几个commit，放到最新commit的后面。
git merge 会把公共分支和你当前的commit 按照提交时间合并在一起，形成一个新的 commit 提交，注意不要在公共分支使用rebase

- 4.

```bash
// 先设置 upstream 为开源项目地址，目的是为了把开源项目的更新 同步到自己fork的项目中
// git remote remove <origin/other> # 一般不用
git remote add upstream https://github.tesla.com/digital-experience/owner-xp-bff.git

//获取更新
git fetch upstream
//合并更新
git rebase upstream/master
//如果有冲突呢 修改文件冲突 修改后git add 冲突文件名 commit提交
git rebase --continue
```  

-5 创建pr 等待维护者审查
打开自己fork的项目 比如 https://github.tesla.com/digital-experience/owner-xp-bff.git
点击pull requests 新建即可 new pull request 

---------------------------------------------------------------------------------------------------------
## Git 提交流程

1. git status  # 查看修改状态
2. git add <file> <file>  # 添加需要提交的文件到 缓存区
3. git stash -u -k  # 忽略其他文件，把忽略文件的修改隐藏，这样提交时不会被提交
4. git commit -m 'CNDE-xxxx : commnets' # 提交到本地仓库
5. git pull # 拉取合并
6. git push # 推送remote 
7. git stash pop # 将本地隐藏恢复，冲突需要合并

## Git Diff 
- 工作区 vs 暂存区 git diff
- 工作区 vs 版本库 git diff head
- 暂存区 vs 版本库 git diff --cached

## Git rebase
> 慎用
- 1. git rebase -i HARD~4  # 修改最近4条commit 注释
	在需要修改的commit line 将pick --> edit :wq 保存
- 2. git commit --amend  # 修改第一条
- 3. git rebase --continue # 继续
- 4. 反复执行 2，3 直到所有4条全修改完成
- 5 git push -f origin <branch> # 强制提交

###
---------------------
修改了4个文件，在不放弃任何修改的情况下，其中一个文件不想提交，如何操作？（没add : git add 已经add: git reset --soft ）
修改到一半的文件，突然间不需要或者放弃修改了，怎么恢复未修改前文件？ (git checkout)
代码写一半，被打断去做其他功能开发，未完成代码保存？(git stash)
代码写一半，发现忘记切换分支了？(git stash & git checkout)
代码需要回滚了？（git reset）
————————————————

## 修改文件暂存 与回复暂存

```bash 
git stash   			# 暂存前，新建file 先，git add <file>
git stash list 			# 查看暂存

git stash clear			# 清空所有暂存的 stash 
```

