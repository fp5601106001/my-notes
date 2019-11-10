设置个人信息
git config --global user.name ""
git config --global user.email ""

--------------------------------------------------------
添加文件
git add ""

提交文件
git commit -m "相关说明"

查看git状态，是否有未提交的修改和新增
git status

查看文件修改了哪些地方
git diff

查看git提交日志
git log (--pretty=oneline)

回退到某个版本
git reset HEAD^
* HEAD表示当前版本，HEAD^表示前一个版本，HEAD~数字标签前100的版本

---------------------------------------------------------

git中有工作区和版本库的概念
1、git add：将文件提交到stage（暂存区）
2、git commit：将修改一并提交到分支（默认master）
* 日常工作是在工作区，文件修改后，通过add存放在暂存区，最后通过commit提交到分支

查看工作区某文件与某分支中该文件的不同。
git diff "版本" -- "文件"

撤销工作区的修改，会撤销到暂存区的版本，如果暂存区没有，就会到最新分支中的版本
git checkout -- "文件名"

删除文件
git rm：删除后，工作区和版本库中就不一致，调用git rm就可以删除版本库中的文件
git commit：提交

--------------------------------------------------------



