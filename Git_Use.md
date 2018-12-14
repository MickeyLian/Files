### git上删除文件夹
* 1、git rm -rf 文件夹名
* 2、git add -A
* 3、git commit -m “delete dir”
* 4、git push
### git上上传项目
* 1、cd 进入你放项目的文件的地址
* 2、输入git init，这个意思是在当前项目的目录中生成本地的git管理（会发现在当前目录下多了一个.git文件夹）
* 3、输入git add . （.的意思是将项目上所有的文件添加到仓库中，如果想添加某个特定的文件，只需把.换成这个特定的文件名即可。）
* 4、git commit -m "first commit"，表示你对这次提交的注释，双引号里面的内容可以根据个人的需要改
* 5、git remote add origin https://自己的仓库url地址（上面有说到） 将本地的仓库关联到github上，
  * #### 附：如果报fatal: remote origin already exists.这个错误
    * 1、先删除远程Git仓库   $ git remote rm origin
    * 2、再添加远程Git仓库   $ git remote add origin https://github.com/MickeyLian/94shoppingmall.git
    * 如果执行 git remote rm origin 还报错的话，我们可以手动修改gitconfig文件的内容
    * $ vi .git/config    把 [remote “origin”] 那一行删掉就好了。（退出 esc ,shift+;）
* 6、输入git push -u origin master，这是把代码上传到github仓库的意思。
### 在git上修改了文件内容，在git上需要的命令：
* git pull
### git 修改文件夹名字
* git mv -f oldfolder newfolder
* git add -u newfolder (-u选项会更新已经追踪的文件和文件夹)
* git commit -m "changed the foldername whaddup"
