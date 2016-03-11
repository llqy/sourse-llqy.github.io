---
title: hexo 部署静态blog于github
date: 2016-03-11 09:56:50
tags:
---
## **配置环境**
OS: win7 64位

安装Node & git:

到[Nodejs.org](http://nodejs.org/) 官网下载安装最新版.

到[git-scm.com](http://www.git-scm.com/)官网下载安装最新版.
## 开始行动
### 注册github
到[github.com](github.com)注册帐号,新建一个`username.github.io`的`repository`.
**username替换成你的用户名**!!必须如此

### 添加SSH key
打开Git Bash(安装git后在开始菜单里有的).
#### 1.首先设置你的用户名密码：
```
git config --global user.email "llqy5251@qq.com"
git config --global user.name "llqy"
```
`llqy5251@qq.com` 改成你的邮箱,此邮箱只是作为之后上传者的身份邮箱,`llqy`改成你的名字.
#### 2.生成密钥：
ssh-keygen -t rsa -C "llqy5251@qq.com"
同上,`llqy5251@qq.com`改成你的邮箱,其实改成其他的也无所谓,不影响后面.
```
$ ssh-keygen -t rsa -C "llqy5251@qq.com"
Generating public/private rsa key pair.
Enter file in which to save the key (//.ssh/id_rsa): H:\git\myssh\ssh
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in H:\git\myssh\ssh.
Your public key has been saved in H:\git\myssh\ssh.pub.
The key fingerprint is:
b0:0c:2e:67:33:ab:c1:50:10:40:0a:ba:c1:80:59:22 llqy5251@qq.com
```
>其中会提示你输入保存key的地址,不改直接回车的话会在默认的c:\users\username,username是你的系统的用户名.

用记事本打开生成的ssh.pub,复制里面的

![ssh.pub](https://neqxoq-sn3301.files.1drv.com/y3m_cGA2-vhx6XwyVvnS5CmYZZpiOtGZMwHU0XpBgoClJYvFJFo7gEJA_JsemD6TvWdaqLjtr2TY91Ygcd91d-w3GbYsa8GTPfq8MOqJkeu_Z1S6jqJQ1VW0c4FQmjQ_tl0-kBc0TX7DmqCRmmIdo2LQzytSX6oTy2A41IHgkJhc4M?width=663&height=118&cropmode=none)

打开[github.com](github.com),如下图
![sitting](https://npqxoq-sn3301.files.1drv.com/y3mrELEkYbSwCqAyCHyoPQTml9emIgIn5UiuqDMtLjsdp_TjGAAM113BHZIbIRh04bNbCExugKOuDYyMNzTsw0JyGPRh2UoxMPd5h3EAjdz8w5_CmoQBYX1yBbBRubrhGOwAkxYf2uwS55bgfLAvItYOPy-T0yNbs91J0fTR9pvQ5U?width=885&height=662&cropmode=none)

最后可以验证一下：
```
$ ssh -T git@github.com
Hi llqy! You've successfully authenticated, but GitHub does not provide shell access.
```
### hexo 生成静态网页
> 参考 [hexo.io](https://hexo.io/zh-cn/)

#### 1.安装 hexo
```
npm install hexo-cli -g
```
#### 2.初始化

然后，执行init命令初始化hexo到你指定的目录：
```
hexo init <folder>
```
> 也可以cd到目标目录，执行hexo init。

好啦，至此，全部安装工作已经完成！

#### 3.生成静态页面

cd 到你的init目录，执行如下命令，生成静态页面至hexo\public\目录。
```
hexo generate
```
命令必须在init目录下执行，否则不成功，但是也不报错。
当你修改文章Tag或内容，不能正确重新生成内容，可以删除hexo\db.json后重试，还不行就到public目录删除对应的文件，重新生成。

本地启动

执行如下命令，启动本地服务，进行文章预览调试。
```
hexo server
```
浏览器输入 http://localhost:4000 就可以看到效果。

#### 4.部署到github

```
npm install hexo-deployer-git --save
hexo d
```
