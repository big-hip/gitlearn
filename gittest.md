git使用



git add添加到暂存区

git checkout 从暂存区移除



git clone /tmp/sample.git  xxx

可以克隆到xxx目录下，指定目录属于是

git remote add origin https://github.com/yourname/project.git
给当前本地 Git 仓库添加一个 远程仓库地址，并起个别名叫 origin。
remote add：添加远程仓库。
origin：是这个远程仓库的代号，你可以用别的名字，但 origin 是默认常用的。
https://...：是远程仓库的真实地址（例如 GitHub 上的仓库地址）。
📌 只是建立“联系”，不会上传代码。

git push -u origin main
作用：
把当前分支（通常是 main）的代码推送到远程仓库 origin 上。

push：推送代码。
-u：设置当前分支与远程分支建立追踪关系，以后可以直接用 git push。
origin：远程仓库名。
main：本地要推送的分支名。
📌 真正上传代码的动作在这一句完成。

你当前的分支是 master，但它还没有对应的远程分支（upstream），所以 Git 不知道你要把它推送到远程仓库的哪个分支上。
所以第一次要 git push -u origin master


git remote add git /tmp/educoder.git
git push -u git master master
第一次这两个要对应


git pull 远程主机名 远程分支名 本地分支名 -f

远程分支和本地分支对同一内容做了修改，这就会导致将远程分支的修改，合并到本地分支的时候发生冲突。这个时候，可以选择解决冲突，然后合并（解决冲突会在后续的实训中介绍）。也可以选择直接强制拉取，使用远程分支的修改，覆盖本地分支的修改。强制拉取需要用到-f参数，


如你本地有master分支和develop分支，目前你正处于develop分支进行开发，现在你想切换到master去，则可以执行下面的操作： git checkout master 这样就能切换到master分支继续进行开发。

git checkout -b brachname   == git branch branchname && git checkout branchname

在开发过程中，很可能出现的一个情况是：你为了解决一个紧急bug，而临时创建了一个分支或者分支过于混乱需要丢弃。这时你就需要进行分支删除操作。

删除本地分支，需要用到git branch命令，且需要-D参数，具体命令格式为：
　　git branch -D 需要删除的分支的名字


删除远程版本库中的某个分支。

删除分支用到的git命令是git push，在具体的使用过程中有不同的用法。

通过推送空分支到远程分支，实现删除。 
推送本地分支到远程分支的方法是： git push 远程主机名 本地分支:远程分支
推送空分支实现删除的方法是：
　　git push 远程主机名 :远程分支
即：前没有指定本地分支名。
#删除远程develop分支，其中origin为远程仓库名
git push origin :develop

通过delete参数删除远程分支：git push 远程主机名 --delete 远程分支名 
#删除远程develop分支,其中origin为远程主机名
git push origin --delete develop