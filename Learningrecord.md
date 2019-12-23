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
五.Git远程仓库的创建  
六.GitHub远程仓库的使用_HTTPS协议  
七.GitHub远程仓库的使用_SSH协议  
八.Git的分支操作  
九.冲突的产生与解决  
十.图形化管理工具  
十一.忽略文件操作