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

