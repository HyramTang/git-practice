# Git 命令速查
## 常用
### init
- `git init`：初始化本地仓库
- `git init --bare`：新建远程仓库
### clone
- `git clone <仓库地址>`：克隆整个仓库
- `git clone <仓库地址> <目录>`：克隆仓库特定目录
### add
- `git add <目录/文件>`：添加指定目录/文件至暂存区
- `git add .`：添加所有内容至暂存区
- `git add -A`：添加所有内容至暂存区
### commit
- `git commit`：提交修改（会打开 [Vim](http://www.runoob.com/linux/linux-vim.html) 编辑器填写提交信息）
- `git commit -m <提交信息>`：提交修改（快速填写提交信息）
- `git commit -am <提交信息>`：所有修改放置暂存区并提交（新增 Untracked 文件无效）
### status
- `git status`：显示文件状态
### log
- `git log`：显示完整提交历史
- `git log --oneline`：精简显示到一行
- `git log --author=<提交者名称>`：查看某人的提交内容
- `git log <文件名>`：查看某个文件的提交内容
- `git reflog`：查看引用的 log，HEAD 移动记录
### show
- `git show`：查看最近一次提交的具体内容
- `git show <提交版本ID>`：查看特定提交版本内容
- `git show <提交版本ID> <文件名>`：查看特定提交版本的文件内容
### config
- `git config --global user.name "Hyram"`：用户名
- `git config --global user.email hyram.tang@gmail.com`：邮箱
- `git config --global --list`：查看全局配置信息
- `git config --global --edit`：修改配置信息
### remote
- `git remote add <仓库地址>`：添加远程仓库地址

## 回滚
### 提交前
- `git reset HEAD <文件名>`：取消已暂存文件（`.` 则取消所有文件）
- `git checkout -- <文件名>`：取消文件的修改内容（`.` 则取消所有文件，仅限未暂存的文件）
- `git stash -u`：暂存所有未提交内容（`-u` 指包含新增 Untracked 的文件）
- `git stash apply`：还原最后一次暂存的内容
### 提交后
- **修正**
	- `git commit --amend`：先修改内容并放置暂存区，执行命令修正**最后一条**的提交内容（会变更提交的版本ID）
	- 修正最后第二个提交太麻烦，具体参考[掘金小册](https://juejin.im/book/5a124b29f265da431d3c472e/section/5a1451dd5188253293142cd7)
- **回退**
	- `git reset --hard HEAD^`：回退到上一个版本（`<提交版本ID>` 则回退到特定版本）
### Push 后
- **自己的 branch**
	- `git push origin <分支名称> -f`：重新编辑提交后或回退提交后，再强制 Push，操作自己的分支不影响其他人。
- **主 branch**
	- `git revert HEAD^`：撤销上一个提交并重新建立版本提交（`<提交版本ID>` 则撤销特定提交）

## 分支
### branch
- `git branch`：列出所有本地分支（`-a` 本地和远程所有分支）
- `git branch <分支名称>`：新建分支
- `git branch -d <分支名称>`：删除分支，仅能删除非当前分支和已经  merge 到 master 的分支（`-D` 强制删除分支）
### checkout
- `git checkout <分支名称>`：切换到特定分支
- `git checkout -b <分支名称>`：新建分支并切换
### merge
- `git merge <分支名称>`：从特定分支 merge 内容至当前分支
- `git merge --abort`：放弃 merge，如果 merge 有冲突，可放弃

## 标签
### tag
- `git tag`：列出所有本地标签
- `git tag <标签名称>`：新建标签并指向最新的提交上
- `git tag <标签名称> <提交版本ID>`：新建标签并指向特定版本上
- `git tag -a <标签名称> -m "<标签提示信息>" <提交版本ID>`：新建标签并增加提示信息指向特定版本上
- `git tag -d <标签名称>`：删除特定标签

## 远程
### remote
- `git remote -v`：查看现有的远程仓库地址
- `git remote add origin <仓库地址>`：给本地仓库添加远程仓库地址
### pull
- `git pull`：拉取远程仓库内容，本质：fetch 后再 merge
### push
- `git push origin`：推送当前分支至远程仓库
- `git push origin <分支名称>`：推送特定分支至远程仓库
- `git push origin -f`：强制推送
- `git push origin --all`：推送所有分支
- `git push origin --tags`：推送所有标签
- `git push origin :feature1`：删除远程分支
- `git push origin :refs/tags/<标签名称>`：删除远程标签
