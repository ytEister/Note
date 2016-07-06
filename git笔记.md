# git常用命令

## git 暂存管理
	git stash # 暂存
	git stash list # 列所有的stash
	git stash apply # 回复暂存的内容
	git stash drop # 删除暂存区

## git 查看文件
	git diff<file> # 比较当前文件和暂存区文件差异
	git diff --staged # 比较暂存区和版本库的差异

## git查看、添加、提交、删除、找回，重置修改文件
	git status # 查看文件的提交状态
	git add # 添加提交的文件
    git add . # 提交所有文件
	git commit -m ‘’ # 提交修改的内容描述
	git pull origin （分支名称） # 拉取远程此分支的更新内容
	git push origin （分支名称）# 将此分支在本地的修改推到远程分支

