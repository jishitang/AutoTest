1、git pull基本用法：

git pull <远程主机名> <远程分支名>:<本地分支名>

例如执行下面语句：

git pull origin master:brantest

将远程主机origin的master分支拉取过来，与本地的brantest分支合并。

上面的pull操作用fetch表示为：

git fetch origin master:brantest
git merge brantest

相比起来git fetch更安全一些，因为在merge前，我们可以查看更新情况，然后再决定是否合并。

2、git push基本用法
git push <远程主机名> <本地分支名>:<远程分支名>

git push origin master
上面命令表示，将本地的master分支推送到origin主机的master分支。如果后者不存在，则会被新建。

如果省略本地分支名，则表示删除指定的远程分支，因为这等同于推送一个空的本地分支到远程分支。


$ git push origin :master
# 等同于
$ git push origin --delete master
上面命令表示删除origin主机的master分支。

如果当前分支与远程分支之间存在追踪关系，则本地分支和远程分支都可以省略。

3、添加远程主机
git remote add <主机名> <网址>
git remote rm <主机名>

4、git fetch
git fetch <远程主机名> <分支名>
比如，取回origin主机的master分支。
$ git fetch origin master

可以使用git merge命令或者git rebase命令，在本地分支上合并远程分支。


$ git merge origin/master
# 或者
$ git rebase origin/master
上面命令表示在当前分支上，合并origin/master。

引言：仓库可以基于源仓库FISCO-BCOS新建一个branch进行开发，也可以从源仓库fork一个自己的仓库在上面作业，以下以fork项目gavinouyang进行介绍
1、git clone 版本库的网址，例如 git clone https://github.com/gavinouyang/FISCO-BCOS.git，此时gavinouyang项目下所有本地分支默认与远程主机的同名分支，建立追踪关系，例如本地的master分支自动"追踪"origin/master分支
	注：追踪的作用是服务于git pull或git push及git fetch，本地和远程没有追踪关系的话，这几个动作会找不到源或目的，不过命令帮助行会给你提醒如何执行跟踪，例如 git branch --set-upstream jishitang origin/jishitang
2、git checkout -b jishitang，以jishitang分支为例。本地工作区（workspace）开始作业，例如做好一个入网register.txt自动化，保存后该自动化就存在jishitang分支本地
3、git add  register.txt，将本地工作区的修改文件提交到暂存区（index或stage）
	注：暂存区的作用是可以是多次保留本地工作区的修改，然后依次提交（commit）
4、git  commit register.txt，将暂存区的修改提交到版本库（jishitang分支本地Repository）
	注：本地版本库记录修改，非实际文件数据，用于和远程版本库和merge本地工作区
以上操作都是本地操作（包括本地工作区和本地仓库）
	
5、git fetch origin master，拉取远程origin主机下master分支到本地库
	注：master不写，默认将远程所有分支拉到本地库。该命令更新的是修改（可以和oracle更改日志类比），非数据
6、git  merge origin/master
	注：将第5步fetch更新的修改，在工作区本机操作，看上去就是merge到本地了
	第5和第6步合并就是 git pull origin master，但不推荐这样使用
	此时本地仓库jishitang分支已经包括了自动化用例修改（git commit）和远程最新代码修改（git merge）
7、git push origin jishitang:maser
	注：将jishitang分支合入master分支（这两个分支都属于gavinouyang项目）
8、提pr请求，将gavinouyang项目下的master分支提到FISCO-BCOS项目某个分支

webase-ide
webase+存证支持
webase-node-mgr


   
	


补充：
git diff是工作区和暂存区的比较，git diff --cached是暂存区和master的比较。
git status是比较本地工作区的变更。



