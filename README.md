git init

>会在文件夹下生成.git
要删除其他的.git,theme目录下的主题都有.git.否则无法add.


git add *

git commit -m "wrote a readme file"

git remote add origin git@github.com:llqy/sourse-llqy.github.io.git


git push -u origin master

git push origin master

git pull origin master

npm install hexo-server --save



其他:
使用git进行版本控制--在多台PC上同步源代码

[日期：2012-08-23]	来源：Linux社区  作者：huzhenwei	[字体：大 中 小]
因为经常把工作带回家去做，在家用电脑上写的一些代码常常来不及与公司电脑上的代码进行同步，导致代码管理混乱。

现在使用git来进行源代码管理，就轻松多了，而且还可以很方便地和别人一起协作开发。

步骤如下：

1. 配置server:

  mkdir repos.git
  cd repos.git
  git --bare init           #建立一个空的 git仓库，--bare 参数说明当前init 的不是工作目录

2. 将PC-1上现有的workspace进行git管理并上传到服务器端:

  cd workspace
  git init
  git add *
  git commit -m 'initial commit'
  git remote add origin ssh://huzhenwei@192.168.1.2/home/huzhenwei/repos.git            #192.168.1.2为服务器的VPN内网IP
  git push origin master        #将本地的代码上传到服务器端

3. 从服务器端检出版本库到PC-2，在PC-2上新建文件并上传到服务器端:

  git clone ssh://huzhenwei@192.168.1.2/home/huzhenwei/repos.git workspace
  cd workspace
  touch newfile         #创建一个新文件来做测试
  git add newfile
  git commit -m 'add newfile'
  git push origin master        #将本地的代码上传到服务器端

4. 在PC-1上获取PC-2更新的内容:

  git pull origin master        #将服务器端的代码下载到本地linux