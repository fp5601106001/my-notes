### 设置个人信息

* 设置用户名：git config --global user.name "用户名"
* 设置邮箱：git config --global user.email "邮箱"

--------------------------------------------------------
### 添加文件

* git add ""

### 提交文件

* git commit -m "相关说明"

### 查看git状态，是否有未提交的修改和新增

* git status

### 查看文件修改了哪些地方

* git diff

### 查看git提交日志

* git log (--pretty=oneline)

### 回退到某个版本

* git reset HEAD^

> HEAD表示当前版本，HEAD^表示前一个版本，HEAD~数字标签前100的版本

---------------------------------------------------------

### git中有工作区和版本库的概念

* git add：将文件提交到stage（暂存区）

* git commit：将修改一并提交到分支（默认master）

> 日常工作是在工作区，文件修改后，通过add存放在暂存区，最后通过commit提交到分支

### 查看工作区某文件与某分支中该文件的差异

* git diff "版本" -- "文件"

### 撤销工作区的修改，会撤销到暂存区的版本，如果暂存区没有，就会到最新分支中的版本

* git checkout -- "文件名"

### 删除文件

* git rm：删除后，工作区和版本库中就不一致，调用git rm就可以删除版本库中的文件
* git commit：提交

--------------------------------------------------------

### 将本地库与远端库关联

* git remote add origin git@github.com:fp5601106001/my-notes.git
* git push -u origin master

> -u:使本地库和远程库关联，下次push的时候就不用加了。相关操作可以参考github上的提示。
>
> 此外，git是基于ssh连接，第一次连接会验证Github服务器的key，主要是通过key，确认远端确实是我们的github服务器。

###  从远程库克隆

* git clone git@github.com:fp5601106001/my-notes.git

> 注意会生成my-notes目录，所以不需要提前新建。

### 分布式协作--分支创建与合并

> 创建分支相当于创建一个指针，然后把HEAD指向这个指针。

* git branch：查看所有分支及当前分支。

* git branch "分支名":创建新的分支
* git checkout "分支名":将HEAD指向该分支名，当前版本就切换到了新的分支

> 以上两条指令可以合为：git checkout -b "分支名"

#### 合并两个分支，并删除dev

* git merge "分支名"：合并分支
* git branch -d dev：删除dev分支

> 实际上checkout在撤销工作区文件修改时已有应用，因此这里可以用switch替换。，如下：

* git switch -c dev：创建dev，并切换到分支dev
* git switch dev：切换到已经存在的分支dev

### 合并冲突的解决

> 当合并出现冲突，git会进入master|Merging分支，这时查看冲突文件会发现冲突的部分，人工合并之后，按照正常的add和commit步骤就可以正常提交。提交后回到master分支

### 查看合并的结构

* git log --graph --pretty=oneline --abbrev-commit

### 分支策略

平时干活的分支管理原则

* master应该是最新最稳定的版本，不能在master上作直接修改；
* 干活都在dev分支上。待开发稳定后，再合并到master分支上，由master分支发布1.0版本。
* 每个人干活都应该有自己的分支，干完活将自己的分支合并到dev分支上；

### bug修复--stash保存现场

bug突发时，需要保存现有的工作环境：

可以在当前工作分支，执行git stash，保存当前的工作环境。然后去修复bug。回来后从stash恢复，然后删除stash即可。

* git stash：创建快照

* git stash list：查看临时保存的工作环境列表

* git stash apply stash@{0}：恢复工作环境

* git stash drop:删除临时存储

* git stash pop：恢复的同时，删除对应的stash

当bug修复需要复制到其他分支时，使用git cherry-pick "序列号"将某次相同的修改应用到其他分支。

### feature分支

> 如果中途发现某开发的功能要取消，在未合并之前，将相应的feature分支删除即可。

* git branch -D "删除的分支"

### 查看远程库信息

* git remote：查看远端库中已push的分支
* git remote -v：查看origin抓取和推送的地址

### 推送本地分支到远程库

* git push origin 分支名：也可以推送dev等其他分支

### 分支管理策略

* master：主分支，必须时刻同步；
* dev：开发分支，团队所有成员都需要在上面工作，也需要同步；
* bug：本地修复，没必要推送，除非有绩效考核；
* feature：是否合作在上面开发同一个功能；

### 多人协作

当多人协作开发时，开发通常是在dev分支上进行

* git clone git@github.com:fp5601106001/repos.git：刚开始是克隆远程库的分支；

* git checkout -b dev origin/dev：刚开始是从远程库拉取并创建dev分支；

* git pull：拉取对应分支的代码；

* git branch --set-upstream-to=origin/分支名 分支名：当pull报错：没有tracking信息的时候，说明本地分支没有与远程库分支建立对应关系。通过这条指令可以建立本地分支与远程分支的链接。

> 当push的时候发生冲突：需要先pull，解决冲突后，再push。

### Rebase

> 用于将本地的分叉提交整理成一条直线，缺点就是本地的分差提交会被修改。

git rebase

### 标签

打标签是为了标识开发版本，通常开发到一定时期，版本稳定的时候，会将相应的版本标识为对外开放的版本。这时就需要打标签来标识相应的版本。

* git tag 版本号 提交id：默认给最新的提交打标签，如果需要给之前的提交打标签，则需要切换到对应的分支，然后，用git log查到提交号，再打标签。
* git show 标签名：标签不会按照时间节点排序，而是字母序。具体时间可以通过git show 查看。
* -m：可以给标签加上说明

#### 标签操作

* git tag -d 标签名：删除某标签

* git push origin 标签名：将标签推送到远程库
* git push origin --tags：将所有全部没有被推送的标签推送到远程库
* git tag -d 标签名   => git push origin:refs/tags/标签名：先删本地，然后再把修改提交到远程库，最后通过github查看是否正常删除。











