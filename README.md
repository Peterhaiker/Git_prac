### 配置系列
`/etc/gitconfig`包含系统每个用户的配置文件，每个用户的主目录下有自己的`~/.gitconfig`文件，每个仓库有针对此仓库的`.git/config`文件，后一级别覆盖前一级别  
#### git config  
```
git config --system
git config --global
git config 
```
带`--system`选项会读取`/etc/gitconfig`文件，带`--global`选项会针对用户，在仓库中不带选项会针对这个仓库  
```
后面再接特定的元素选项，比如：
user.name usrname
user.email xxx@@@.com
core.editor editorname
...
```
```
列出配置信息
git config --list
```
### 获取仓库
#### git init:
将当前所在目录初始化为git仓库，交由git管理，创建了.git目录  
#### git add \<filename\>  
将工作区的文件交到暂存区  
#### git commit -m "注释"  
将暂存区的文件交到本地仓库，注释要写清楚这次的改动  
#### git commit -a m "注释"  
同上，不同的是直接从工作区交到本地仓库，前提是提交的文件曾经交给过本地仓库  
#### git clone url
将远程仓库克隆到本地，新目录名就是仓库名。如果你想自定义名字在url后加上空格和目录名就可以了  
#### git status:  
检查当前文件状态，此命令非常有用，当我们不知道该干嘛时，不妨敲这个试一下  
#### git diff:  
默认比较工作区和本地仓库最后一次提交的版本的比较  
#### git diff --staged  
比较暂存区和本地仓库最后一次提交的版本的比较,也可以用\-\-cached来代替\-\-staged  
#### git rm \<filename\>  
从暂存区移除文件,连带着工作区的也被删除，然后提交，这样就不会出现未跟踪状态  
    * -f选项表示强制删除，不可恢复  
    * --cached选项表示只删除暂存区的，不删除工作区的  
#### git mv \<oldfile\> \<newfile\>  
重命名一个文件，不会出现未暂存的情况  
#### git log  
显示提交的历史记录，有许多参数，可定制显示方式  

### 撤销系列命令  
#### git commit --amend
    当你发现还有文件未提交想重新提交时，这个命令可以将这次的提交和上次的提交合并  
#### git checkout -- <filename>  
    当工作区的文件被修改了，想要回退到上一个版本，用此命令  
#### git stash  
    同上，区别是上一个命令操作之后不可再后悔，也就是你回退以后不能反悔你这个回退，但是git stash可以  
#### git stash apply  
    将上一个回退的命令行为(git stash)撤销，配合git stash使用  
#### git reset HEAD\<file\>  
    当在工作区修改过的文件被提交到暂存区，想要重新回退到工作区也就是提交之前修改之后的状态，用此命令  
#### git reset --hard\<哈希值\>  
    如果被修改的文件已经交到本地仓库，那么此命令能将仓库中这个文件回退到哈希值指定的那次提交  

### 远程仓库
#### 查看远程仓库
* git remote  
    origin是默认的远程仓库名，若已克隆则会有此字眼  
* git remote -v  
    显示远程仓库名和url，如果远程仓库不止一个则会列出所有的  
#### 添加远程仓库的别名
* git remote add \<shortname\> <url>  
    添加一个新的远程仓库同时指定一个你可以轻松引用的简写  
#### 推送到远程仓库  
* git push
推送所有分支
* git push destination origin  
将本地仓库origin推送到远程仓库destination(这里的destination表示远程仓库，默认通常是origin).默认不推送标签，除非加`--tags`选项  
* git push -u destination origin  
指定destination为以后推送的默认仓库，这是在有多个远程仓库和本地仓库相连的情况下需要考虑的  
#### 创建远程仓库
* git push origin local_branch
创建远程分支，origin是远程分支名,local branch必须是本地已创建的分支名  
* git push origin :remote_branch  
先删除本地分支，在删除远程分支
#### 从远程仓库中抓取与拉取  
* git fetch [remote-name]  
它会将远程仓库中比本地新的文件拉取下来  
* git fetch origin master:A
拉取远程仓库到本地的A分支
#### 查看远程仓库  
* git remote show [remote-name]  
查看远程仓库的详细信息  
#### 远程仓库的移除与重命名  
* git remote rename \<oldname\> \<newname\>  
* git remote rm \<repository name\>  
### tag标签相关  
#### git tag -a\<tag name\> -m "tag comment"  
给当前最近一次的提交打上标签。tag name是标签名，tag comment是给标签添加 的注释  
#### git tag -a <tag name> -m "tag comment" <哈希值>  
同上，一样是打标签，但是这次给提供的hash值指定的提交打上标签  
#### git tag  
列出你的所有标签  
#### git show <tag name>  
列出tag name指定的那次提交的详细信息  
### 分支相关  
* 在*/.git/refs/heads/目录下有多少文件就有多少分支  
* 切换分支就是改变.git目录下的HEAD文件的内容  
* [四种git合并分支方法](http://yanhaijing.com/git/2017/07/14/four-method-for-git-merge/)  
#### git branch  
列出分支，删除分支  
#### git branch\<branch name\>  
创建分支  
#### git branch -d <branch name>  
删除指定的分支,但是如果你要删除的分支中有比主分支还新的文件则会报错  
#### git branch -D <branch name>  
同上，，但是解决上一个命令报错的情况，强制删除  
#### git checkout <branch name>  
切换到另一个分支  
#### git checkout -b \<branch name\>  
同上，但是如果指定的分支不存在，则创建并切换  
#### git merge  
将一个分支合并到当前分支  
#### git cherry-pick 哈希值  
将另一个分支上指定的文件合并到当前分支  
### 快速推进  
分支合并还是分支，但快速推进合并就是真正合并为一条直线没有分叉,按如下步骤顺序进行  
#### git rebase <branch1> <branch2>  
基于branch1来重做branch2，就是在branch1后面加上branch2新增的，然后branch2就是这个新形式的分支(不是另外创建了一个分支)  
####  git checkout branch1  
切回branch1分支  
#### git merge branch2  
将刚刚更新的branch2合并到所在的分支  
___________________________
至此成功，但是如果branch1和branch2有同名文件但内容修改的不同则合并时会冲突，此时您会在它创建的临时分支内等待您来解决冲突  
1：首先用编辑器打开冲突的文件解决冲突后(编辑一下文件)保存退出  
2：执行git add <冲突文件名>  
3：运行git rebase --continue  
4：git checkout branch1  
5：git merge branch2  
