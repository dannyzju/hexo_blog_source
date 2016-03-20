---
title: 利用Hexo快速搭建GitHub博客
date: 2016-03-20 01:05:03
tags:
- hexo
---
目前基于GitHub的博客框架有不少，比如JekyII，Octopress等， 但相对来说Hexo上手简单，并且更加快速，简洁且高效，可以让我们更加专注于写作本身。


#### Step 1: 创建GitHub Repository
登陆GitHub，并且创建一个新的repository。
需要注意的是这个repository的名字必须是username.github.io的形式。比如说我的用户名是dannyzju，那么在这里我的repository 的名字就必须是dannyzju.github.io。
![Create a new repository](/content/images/2016/createGitHubBlogWithHexo.png)
确认repository名字无误后，点击 Create repository按钮。

#### Step 2: 安装hexo
在开始安装hexo之前，需要确定Mac上已经装好：
- [Node.js](http://nodejs.org)
- [Git](https://git-scm.com)

接下来打开terminal，输入如下指令安装hexo：

```bash
npm install hexo-cli -g
```
安装完成后，输入以下三行命令初始化博客：

```bash
hexo init blog 
cd blog
npm install
```

本地hexo的安装就完成了，输入以下命令即可在本地预览。
```bash
hexo server
```
#### Step 3: 将博客部署到github上
首先需要在terminal中输入以下命令，安装 hexo-deployer-git
```bash
npm install hexo-deployer-git --save
```
在刚才安装博客的blog文件夹下找到_config.yml， 用文本编辑器打开。
在最后可以看到deploy的初始设置信息如下：
```bash
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
	type:
```
回到github我们刚才创建的repository页面，复制repository的url。
然后修改_config.yml的deploy设置如下：
```bash
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: git
  repo: https://github.com/username/username.github.io.git
  branch: master
```
保存修改并退出。

打开terminal，进入创建的blog文件夹路径，依次输入以下命令：
```bash
hexo clean
hexo generate
hexo deploy
```

到此为止，个人博客就已成功部署到github上了。打开username.github.io，就可以看到刚才创建的博客了。

#### Step 4: 个性化设置
我们可以在_config.yml中对博客进行进一步的设置。
首先用文本编辑器打开_config.yml文件，第一个section是博客页面的基本信息，我们可以修改如下：
```bash
# Hexo Configuration
## Docs: https://hexo.io/docs/configuration.html
## Source: https://github.com/hexojs/hexo/

# Site
title: D.Z. Notes
subtitle: 不苛求完美，不停止进步。
description:
author: Danny Zhang
language: en
timezone:
```

接下来我们可以尝试更换博客的主题风格，在这里以Maupassant主题为例：
在terminal中进入创建的blog文件夹，依次输入以下命令：
```bash
$ git clone https://github.com/tufu9441/maupassant-hexo.git themes/maupassant
$ npm install hexo-renderer-jade --save
$ npm install hexo-renderer-sass --save
```
然后在_config.yml中修改theme设置如下：
```bash
# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
theme: maupassant
```

保存文件并退出。
在terminal的blog路径下，依次输入以下命令：
```bash
hexo clean
hexo generate
hexo deploy
```
刷新博客页面，就可以看到网站信息和主题已经被更新了。


#### Step 5: 发布博文

在terminal中输入以下命令：
```bash
hexo new "文章题目"
```
命令执行完后，就会发现在/blog/source/_post中多了一个“文章题目.md"文件，这就是我们刚才新建的博文。
Hexo支持markdown格式的文档，我们可以使用文本编辑器(如Sublime Text)或者markdown编辑器(如chrome app Marxico)，实现博文更新。

最后，再次执行下面几条命令，将博客部署到GitHub上：

```bash
hexo clean
hexo generate
(若要本地预览就先执行 hexo server)
hexo deploy
```

刷新博客页面，就可以看到博文更新啦 ：）

#### End
- 更多的Hexo设置请参考Hexo官方文档：
	- https://hexo.io/docs/
- Maupassant主题的GitHub页面：
	- https://hexo.io/docs/
- 需要更详细的搭建指南也可参考以下文章：
	- [如何利用GitHub Pages和Hexo快速搭建个人博客](http://sunwhut.com/2015/10/30/buildBlog/?hmsr=toutiao.io&utm_medium=toutiao.io&utm_source=toutiao.io)
	- [Windows下一步步搭建自己的独立博客——使用 GitHub Pages + Hexo 基础教程](http://yangruihan.com/2015/03/22/Windows下一步步搭建自己的独立博客——使用%20GitHub%20Pages%20+%20Hexo%20基础教程（一）/)

