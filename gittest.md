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



git checkout -b brachname  == git branch branchname && git checkout branchname



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

\#删除远程develop分支，其中origin为远程仓库名

git push origin :develop



通过delete参数删除远程分支：git push 远程主机名 --delete 远程分支名 

\#删除远程develop分支,其中origin为远程主机名

git push origin --delete develop



分支合并需要用到git merge命令，具体的命令格式为：

　　git merge 需要合并的分支

在具体使用中，如当前处于master分支，需要将develop分支合并到master分支，则具体的使用方式如下：

　　git merge develop



默认快进式合并，正常合并会产生一个新的节点

log在正常合并里面会有一个分叉

git merge --no-ff develop



git merge branch-name 时，Git 会检查当前分支（如 master）的历史中是否已经包含了 branch-name 的所有提交。如果是，则认为该分支已被合并，执行 快进合并（Fast-forward） 或直接跳过合并。



当你执行 git revert 命令后，Git 会做以下事情：

创建一个新的提交，这个提交的内容与你要撤销的提交正好相反

自动打开默认的文本编辑器，让你编辑撤销提交的说明信息

保存并关闭编辑器后，这个撤销操作就会被记录为一次新的提交



几种模式的具体使用方法如下：





撤销修改



\#直接丢弃工作区和暂存区的修改

git reset --hard HEAD

\#暂存区内容保留，工作区修改丢弃

git reset --mixed HEAD

\#暂存区和工作区内容都保留

git reset --soft HEAD



删除文件



但是无论使用哪种方式，都相当于在本地做了修改，在git rm --cached之后，使用git status查看版本库状态，可以得到如下输出：

因此，还需要通过git commit操作将修改提交。



在开发过程中，commit ID是一串无序的字符，它虽然能唯一标记一次代码提交，即一个版本。但是，它很难记忆和辨识。所以，为了给不同的版本起一个容易辨识的名字，我们可以给这次提交打上一个标签，用不同的标签来对应不同的版本。这样，就相当于给这次提交生成了一个快照。实际上，在为某次提交创建标签的时候，Git会为标签生成一个指针，以指向其对应的提交。然后，我们就可以通过标签找到对应的提交，这样对我们版本发布和代码审查都很有帮助。



git tag -a v1.0 -m "版本1.0"



查看标签

查看标签需要用到git tag命令，其具体使用示例如下:

git tag



这样就能列出所有的标签，显示的标签按字母顺序排列，所以标签的先后并不表示重要程度的轻重。



如果标签过多，而你指向显示指定的某些标签，则可以使用正则表达式：



git tag -l 'v5.1.2.*'

如上，使用-l参数，并使用v5.1.2.**这一正则表达式，就过滤除了符合要求的标签，其中v5.1.2.**为正则表达式，它能够匹配所有前缀为v5.1.2的标签。



创建标签

不含附注的标签

创建标签的命令格式为：



git tag 标签名 commitID

参数commitID标识了该标签对应的代码版本，如果不提供commitID，就默认为最近一次提交后的代码打标签。



包含附注的标签

如果需要像提交代码时增加提交日志那样，为每个标签添加说明信息，则需要使用：



git tag -a 标签名 -m "说明信息"





推送指定标签到远程仓库的Git命令如下：



git push 远程主机名 tag名

其中，远程主机名为远程Git版本库对应的主机名，tag名为准备推送的标签名。



该命令使用示例如下：



git push origin v1.0

该语句表示将v1.0标签，推送到主机名为origin对应的远程仓库。



推送全部标签

推送指定标签需要用到：

git push 远程主机名 --tags

其使用方法如下：

git push origin --tags

其中origin为远程主机名，这样就能将全部标签推送至远程仓库。





删除本地标签

删除本地标签，需要用到的命令格式为：



　　git tag -d 标签名

具体使用方法示例如下：



　　git tag -d v1.0

这样就能实现删除v1.0标签。

\#####删除远程标签



删除远程tag，可以使用如下命令：



git push origin --delete tag 标签名





冲突有内容冲突和树冲突，树冲突是改名引起的



即解决冲突的一般过程为：

手动编辑冲突区域；

执行git add，将编辑提交到暂存区；

执行git commit，将编辑提交到本地仓库以解决冲突。



备份当前本地分支（可选）：

为了防止数据丢失，您可以先创建当前分支的备份：



git branch backup-branch



这将创建一个名为 backup-branch 的分支，保存当前分支的状态。



获取远程分支的最新内容：



git fetch origin



这会从远程仓库获取最新的分支信息，但不会自动合并。



重置本地分支以匹配远程分支：



git reset --hard origin/<branch-name>



将 <branch-name> 替换为您要同步的分支名称（例如 main 或 master）。此命令会将本地分支重置为远程分支的状态，丢弃所有本地更改。



### **1. 删除本地的远程跟踪分支（推荐方式）**

使用 `git branch -d -r` 命令（`-r` 表示远程分支，`-d` 表示删除）：

```bash
git branch -d -r origin/branch-name
# 简写形式
git branch -dr origin/branch-name
```

**示例**：删除本地跟踪的远程分支 `origin/feature-old`

```bash
git branch -dr origin/feature-old
```

### **2. 通过 `git fetch` 自动清理（更彻底）**

使用 `git fetch --prune`（或简写 `git fetch -p`）命令，它会在获取最新远程分支信息的同时，自动删除本地已不存在的远程跟踪分支：

```bash
git fetch --prune origin
# 简写
git fetch -p origin
```


**场景**：当远程仓库中的分支被删除后，执行此命令可同步清理本地的过时跟踪分支。

如果你在本地版本库里，放入了仅供本地测试用的文件，但是你并不想将其推送到远程仓库，而且不想每次都被提醒你本地有未提交文件的话，就需要用到Git忽略文件提醒的功能。

在Git工作区的根目录下，创建一个特殊的.gitignore文件，把要忽略的文件名或者文件名的通配符填进去，然后将.gitignore提交到本地仓库，这样Git就会在你添加或者提交时，自动忽略这些文件。

如果我们需要自己定义忽略哪些文件，就需要将其添加到.gitignore文件中去。你可以使用文件的全称，或者使用正则匹配的通配符。如下所示：

# 忽略指定文件
HelloWrold.class
# 忽略指定文件夹
bin/
bin/gen/
# 忽略.class的所有文件
*.class
# 忽略名称中末尾为ignore的文件夹
*ignore/
# 忽略名称中间包含ignore的文件夹
*ignore*/