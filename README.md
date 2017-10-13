﻿[常用命令](#常用命令)  
[撤销系列命令](#撤销系列命令)  
[tag标签相关](#tag标签相关)  
[杂项](#杂项)  

## 常用命令
### git init  
    将当前所在目录交由git管理，创建了.git目录
#### git status:  
    查看当前管理的目录的状态，看看是否有修改过未提交的等等
### git add \<filename\>  
    将工作区的文件交到暂存区
### git commit -m "注释"  
    将暂存区的文件交到本地仓库，注释要写清楚这次的改动
### git commit -a -m "注释"  
    同上，不同的是直接从工作区交到本地仓库，前提是提交的文件曾经交给过本地仓库  
### git log  
    显示提交的历史记录  
## 撤销系列命令  
### git checkout -- \<filename\>  
    当工作区的文件被修改了，想要回退到上一个版本，用此命令  
### git stash  
    同上，区别是上一个命令操作之后不可再后悔，也就是你回退以后不能反悔你这个    回退，但是git stash可以  
### git stash apply  
    将上一个回退的命令行为(git stash)撤销，配合git stash使用  
### git reset HEAD\<file\>  
    当在工作区修改过的文件被提交到暂存区，想要重新回退到工作区也就是提交之前    修改之后的状态，用此命令  
### git reset --hard\<哈希值\>  
    如果被修改的文件已经交到本地仓库，那么此命令能将仓库中这个文件回退到哈希值指定的那次提交  
    
## tag标签相关  
### git tag -a\<tag name\> -m "tag comment"  
    给当前最近一次的提交打上标签。tag name是标签名，tag comment是给标签添加     的注释  
### git tag -a \<tag name\> -m "tag comment" <哈希值>  
    同上，一样是打标签，但是这次给提供的hash值指定的提交打上标签  
### git tag  
    列出你的所有标签  
### git show \<tag name\>  
    列出tag name指定的那次提交的详细信息  
## 分支相关  
* 在*/.git/refs/heads/目录下有多少文件就有多少分支  
* 切换分支就是改变.git目录下的HEAD文件的内容  
* [四种git合并分支方法](http://yanhaijing.com/git/2017/07/14/four-method-for-git-merge/)  

### git branch  
    列出分支，删除分支  
### git branch\<branch name\>  
    创建分支  
### git branch -d \<branch name\>  
    删除指定的分支,但是如果你要删除的分支中有比主分支还新的文件则会报错  
### git branch -D \<branch name\>  
    同上，，但是解决上一个命令报错的情况，强制删除  
### git checkout \<branch name\>  
    切换到另一个分支  
### git checkout -b \<branch name\>  
    同上，但是如果指定的分支不存在，则创建并切换  
### git merge  
    将一个分支合并到当前分支  
### git cherry-pick 哈希值  
    将另一个分支上指定的文件合并到当前分支  
### 快速推进  
分支合并还是分支，但快速推进合并就是真正合并为一条直线没有分叉,按如下步骤顺序进行  
### git rebase \<branch1\> \<branch2\>  
    基于branch1来重做branch2，就是在branch1后面加上branch2新增的，然后branch2就是这个新形式的分支(不是另外创建了一个分支)  
### git checkout branch1  
    切回branch1分支  
### git merge branch2  
    将刚刚更新的branch2合并到所在的分支  
至此成功，但是如果branch1和branch2有同名文件但内容修改的不同则合并时会冲突，此时您会在它创建的临时分支内等待您来解决冲突  
1. 首先用编辑器打开冲突的文件解决冲突后(编辑一下文件)保存退出  
2. 执行git add <冲突文件名>  
3. 运行git rebase --continue  
4. git checkout branch1  
5. git merge branch2  

## 杂项  
### git diff:  
    默认比较工作区和本地仓库最后一次提交的版本的比较  
### git diff --staged  
    比较暂存区和本地仓库最后一次提交的版本的比较  
### git rm \<filename\>  
    从暂存区移除文件  
### git mv \<oldfile\> \<newfile\>  
    重命名一个文件  
