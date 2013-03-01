#git github
##git 第一次运行时设置
```sh
$ git config --global user.name "Your Name"
$ git config --global user.email your.email@example.com
$ git config --global core.editor "gvim -f" #设置默认编辑器
$ git config --global alias.co checkout #用 co 代替字数较多的 checkout 命令
```
##日常应用

```sh
$ git init #新建仓库
$ git add . #把 Rails 项目中的文件添加到 git 的暂存区域（staging area）
$ git status  #查看暂存区域
$ git commit -m "评论" #用 commit 命令告诉 git 你想保存这些改动
$ git log #查看提交的历史信息
```
##文件删除与恢复
```sh
$ rm -rf app/controllers/ #删除文件或其他改动
$ git status  #查看改动
$ git checkout -f  #覆盖当前改动
```

##github
###［创建 SSH 密匙］（https://help.github.com/articles/generating-ssh-keys）

###创建公共项目并推送

git remote add origin https://github.com/laoguo1986/bjjl.git

git push -u origin master

git push  #大多数系统中我们都可以省略 origin master，只要运行 git push
##分支，编辑，提交，合并
```sh
$ git checkout -b sonbranch #创建子分支
$ git branch  #查看当前分支
$ 改动子分支
$ git checkout master  #回到主分支
$ git merge sonbranch #合并分支
$ git branch -d sonbranch #合并分支
$ git branch -D topic-branc #使用 git branch -D 放弃对从分支所做的修改,和旗标 -d 不同，即使还未合并 -D 也会删除分支。
```
###部署

$ gem install heroku 

$ heroku keys:add

$ heroku create --stack cedar #在 Heroku 上新建一个应用程序

$ git push heroku master #通过 Git 将应用程序推动到 Heroku 中

$ heroku open #通过 heroku create 命令给出的地址,查看你刚刚部署的应用程序

