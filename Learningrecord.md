一.Git介绍  
Git是由C语言开发的分布式版本控制系统。Git本地操作有三个区域：工作区：添加、编辑、修改文件等操作；暂存区：暂存已经修改的文件最后统一提交到git仓库中；Git Repository(Git仓库)：最终确定的文件保存到仓库，成为一个新的版本，并且对他人可见。  

二.Git安装    
1.从官网直接下载安装程序，按照默认选项安装。官网地址：https://git-scm.com/  
安装完成后，桌面空白处右键点击鼠标找到Git Bash，在命令行中输入基本信息：用户名和邮箱。  
$ git config --global user.name "Robin"  
$ git config --global user.email "0000000000@qq.com"  
git config命令中 --global参数，表示本台机器上所有的Git仓库都会使用该配置。  

三.Git本地仓库操作  
当需要让Git管理新目录或者已存在目录时，需要创建仓库。可以是空目录也可以是非空目录。并且为了避免出现意外问题，不能使用含中文的目录。    
步骤1：创建空目录时。可直接使用mkdir命令创建。  
步骤2：进入该目录。可直接使用cd命令到该目录下。  
步骤3：Git仓库初始化。可使用git init命令。  
初始化的目的可以理解为，告诉Git需要它来管理这个目录。  
$ mkdir filename  
$ cd filename  
$ git init  
初始化完成后将隐藏文件展示出来即可看到名为.git的文件。此时git仓库已经初始化完成。  

四.Git基本操作  
1.Git常用指令操作  
查看当前状态：git status  
添加到缓存区：git add filename.md  
说明：git add命令，可以添加一个文件，也可以同时添加多个文件。  
语法1：git add filename.md 添加1个名为filename的文件  
语法2：git add filename1.md filename2.md :添加多个指定文件，文件名之间用空格隔开。  
语法3：git add . 添加当前目录到缓存区中，注意.之前必须写空格。  
提交至版本库：git commit -m "注释内容"  
2.版本回退  
版本回退分为两步骤进行操作：  
步骤1：查看版本，确定要回到的时刻点。  
命令：(推荐使用第二个写法，直观)  
git log  
git log --pretty=oneline  
步骤2：回退操作。  
命令：  
git reset --hard 版本号  
注意：回到过去版本之后，如果想再回到最新版本的时候，需要使用命令去查看历史操作，以得到最新的 commit id。  
命令：git reflog  
3.版本差异比较  
如果在git status时发现文件被修改，可通过命令查看制定文件的具体修改内容。  
命令：git diff filename.md  
4.撤销修改  
当你想要撤销工作区修改时，可以使用命令将指定文件在工作区的修改全部撤销。  
命令：  
git git restore filename.md  
若已经提交至暂存区可使用命令git restore --staged filename.cd把暂存区的修改撤销掉，重新放回工作区。  
旧版中：  
git checkout -- filename.md命令中的--很重要，没有--，就变成了“切换到另一个分支”的命令。  
命令git checkout -- filename.md意思就是，把filename.md文件在工作区的修改全部撤销，有两种情况：  
情况1：filename.md自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；  
情况2：filename.md已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。  
若已经提交至暂存区可使用命令git reset HEAD filename.md把暂存区的修改撤销掉，重新放回工作区。  
git reset命令既可以回退版本，也可以把暂存区的修改回退到工作区。当我们用HEAD时，表示最新的版本。  
5.删除文件  
若将文件管理器中的某文件删除，则工作区和版本库就不一致了，git status命令会立即告诉用户哪些文件被删除了。则需要执行以下命令：  
$ git rm filename.md  
$ git commit -m"移出**文件"  
注意：git rm <file> 和 git add <file>效果相同。  
如果 该文件是误删，未提交至版本库，则可使用git checkout恢复至版本库版本。  
$ git checkout -- filename.md  
git checkout 是用版本库的版本替换工作区版本。  

五.GitHub远程仓库的使用  
以GitHub为例，首先，create a new repository。  
1.基于HTTPS协议  
a.本地创建一个空目录，名称命名为filename，并且cd到该目录下。  
b.使用clone命令克隆线上仓库到本地并鉴权  
语法：git clone 线上仓库地址  
首次向线上仓库提交内容时会出现403错误，原因是不是任何人都可以往线上仓库提交内容，必须鉴权。  
需要修改"git/config"文件内容：  
[remote "origin"]
	url = https://用户名:密码@github.com/ZCYRobin/GitLearningrecord.git
	fetch = +refs/heads/*:refs/remotes/origin/*  
c.在仓库上做对应的操作（提交暂存区、提交本地仓库、提交线上仓库、拉取线上仓库）  
提交线上仓库命令为：git push  
如果push后未出现fatal错误则表示提交成功。  
拉取线上仓库命令为：git pull  
养成第一件事先git pull的好习惯，避免出现修改冲突。并且要记得及时提交。  
2.基于SSH协议【推荐使用】  
该方式与http方式相比，只影响github对于用户的身份鉴权方式，对git的具体操作无影响。  
a.生成客户端公私钥文件  
生成公私钥对指令（需先自行安装OpenSSH）：ssh-keygen -t rsa -c "注册邮箱"
b.将公钥上传到github  
找到公钥所在文件id_rsa.pub 用编辑器打开，把该内容复制，粘贴到浏览器中显示的指定位置，title随意。  
c.执行后续git操作，操作和之前相同，先git clone到本地。  

六.Git的分支操作  
分支相关指令：  
查看分支：git branch  
创建分支：git branch 分支名  
切换分支：git checkout 分支名  
删除分支：git branch -d 分支名  
合并分支：git merge 被合并的分支名  
查看分支命令执行后，当前分支前面会有一个标记"*"并且会有颜色标记。  
对于新分支，可以使用"git checkout -b 分支名"指令来切换分支，-b选项表示创建并切换，相当于是创建分支和切换分支两个操作命令。  
删除分支时，必须先退出要删除的分支。  
注意本地分支操作后还是要记得及时push。  

七.冲突的产生与解决  
1.先git pull  
2.修改后重新提交  

八.图形化管理工具  
1.Github for Desktop  
2.Source tree  
3.TortoiseGit  

九.忽略文件操作
在git工作区根目录下创建一个特殊的.gitignore文件，该文件用于声明忽略文件或不忽略文件规则，该规则对当前目录及其子目录生效。  
注意，该文件因为没有文件名，没有办法在windows目录下直接创建，可通过命令行Git Bash 来 touch 创建。命令：$ touch .gitignore  
然后把需要忽略的文件名填写进去，git就会自动忽略这些文件。直接用编辑器打开.gitignore文件写规则，例如：  
#忽略掉/js目录  
/js/  
常见规则写法有以下几种：  
1./mtk/			过滤整个文件夹  
2.*.zip			过滤所有.zip文件  
3./mtk/do.c		过滤某个具体文件  
4.!index.py		不顾虑具体某个文件  
在文件中，以#开头的都是注释。
