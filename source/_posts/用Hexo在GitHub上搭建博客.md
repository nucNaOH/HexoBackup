---
title: 用Hexo在GitHub上搭建博客
date: 2016-07-14 12:08:54
tags: Hexo, GitHub
---
最近学习了使用hexo在GitHub上搭建博客，特此记录。
## 需要安装的软件
1. [node.js](https://nodejs.org/en/)
2. [Git](https://git-scm.com/downloads)
<!-- more -->

## Git与GitHub相关
#### 注册并创建GitHub仓库
仓库名字格式应为：`githubname.github.io`，类型为`Public`即可。创建成功后会生成该仓库的git地址，格式如下：
> https://github.com/your_name/your_name.github.io.git

#### Git本地配置
在本地Git Bash中配置个人名字和邮箱，用来记录提交信息。
``` bash
$ git config --global user.name "your_name"
$ git config --global user.email "your_email@your_email.com"
```
#### SSH key配置
SSH key是用来将本地Git与远程的GitHub关联起来的关键配置。在本地Git bash中执行如下命令：
#### 1. 检查SSH key的设置
``` bash
$ cd ~/.ssh
```
#### 2. 备份并移除原来的SSH key
``` bash
$ ls
$ mkdir key_backup
$ cp id_rsa* key_backup
$ rm id_rsa*
```
#### 3. 生成新的SSH key
``` bash
$ ssh-keygen -t rsa -C "your_email@your_email.com"
```
#### 4. 添加SSH key到远程GitHub
生成的*id_rsa*是私钥，需要保管好，而公钥*id_rsa.pub*中的内容需要在个人GitHub主页的Settings里的SSH and GPG keys选项中添加上，title项可根据个人习惯随便写。
#### 5. 测试
``` bash
$ ssh -T git@github.com
```

## Hexo的安装与使用
#### 安装Hexo
Hexo是一个快速、简洁且高效的博客框架。在安装完node.js之后，就可以在命令行或git bash中使用npm命令进行安装Hexo了。
``` bash
$ npm install hexo-cli -g
```
#### 使用Hexo
安装完hexo后，在需要的文件夹下（以F:/Hexo为例）右键->"Git Bash Here"，在git bash中输入如下命令
``` bash
$ hexo init "your_blog"
$ hexo g
$ hexo s
```
在浏览器中打开<http://localhost:4000>便能在本地预览博客效果

## 发布博客到GitHub Repo
#### 本地仓库跟GitHub建立联系
在Hexo生成的.deploy_git文件夹下用git将其与远程仓库建立联系（只需要执行一次）
``` bash
$ git init
$ git remote -v
$ git remote add origin git@github.com:your_name/your_name.github.io.git
```
#### 发布博客
``` bash
$ hexo g
$ hexo d
```
Hexo还有很多好用的模板可供使用，详细的使用方法此处仅贴几个相关链接，供后续学习使用。
## 相关链接
[Hexo theme](https://github.com/hexojs/hexo/wiki/Themes)
[Hexo github](https://github.com/hexojs/hexo)
[Hexo 官网](https://hexo.io/zh-cn/)

