安装好git工具，在D盘创建一个目录gitlab
运行git bash，进入命令行界面

cd /d/igtb

git init 
git clone git@gitlab-project-url.git

git branch
//查看本地分支

git branch -a

git branch -r

git checkout -b dev
从master切换到dev分支

git add file1 file2 ……
添加变更文件至提交区

git add .
添加所有变更至提交区

git commit -am “备注”
提交提交区的变更文件至本地仓库

git push
推送本地代码至远端仓库

git tag
展示当前项目的所有标签

git tag -a tagname -m “备注”
给当前项目本地最新版本打标签

git tag -a tagname -m “备注” 版本hash值
给当前项目本地的历史版本带标签

git push origin tagname
推送版本的标签至远端仓库

git tag -d tagname
删除本地版本的标签

git push origin -d tagname
删除远端仓库的版本标签
