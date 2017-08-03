---
title: Hexo + Github Pages 博客
categories:
  - Hexo
tags:
  - Hexo
  - Github Pages
  - Git
date: 2017-08-03 14:58:35
---
Hexo是一个博客框架，用来生成静态博客，利用Git工具，可以将博客部署到Github Pages上。
# Github Pages 创建
根据Github的帮助文档设置自己的Github Pages，[Help](https://help.github.com/articles/configuring-a-publishing-source-for-github-pages/)。
# 安装Hexo
根据Hexo的帮助文档安装Hexo，[help](https://hexo.io/zh-cn/docs/)。
# 配置Hexo
在本地生成Hexo站

    hexo init \<folder\>
    cd \<folder\>
    npm install

## 下载Hexo主题
这里使用NexT主题，[NexT](https://github.com/iissnan/hexo-theme-next)。
## 设置主题
设置站点配置文件_config.yml，使用NexT主题

    theme: next
## 添加分类、标签页面
Hexo的分类、标签页面要自己添加。

    hexo new page categories
    hexo new page tags
在分类页面，添加"categories"类型

    title: 分类
    date: 2014-12-22 12:39:04
    type: "categories"
    comments: false
在标签页面，添加"tags"类型

    title: 标签
    date: 2014-12-22 12:39:04
    type: "tags"
    comments: false
## 设置菜单
编辑主题配置文件，设置

    menu:
      home: /
      categories: /categories/
      #about: /about/
      archives: /archives/
      tags: /tags/
      #sitemap: /sitemap.xml
      #commonweal: /404/
# 部署Hexo
生成表态博客页面后，编辑站点配置页面，在deploy段设置git推送信息

    type： git
    repo: git@github.com:xxx/xxx.github.io.git
    branch: master
这里xxx表示对应的git库名称，再在Git Bash窗口执行Hexo指令

    hexo d
来进行部署。
# 多机共享环境
用Hexo配置好站点后，只能在当前配置好的环境下编辑、发布博客，要在多个电脑上都能进行编辑和发布，一个思路是把建立的博客站点中重要的文件备份并推送到Github上，如果在新的环境中，安装好Hexo后，建立一个空的站点，把Github上的文件签出，就可以建立一个同步的编辑环境。
## 初始设置Github库
在创建好Github Pages后，新建一个分支用来保存Hexo原始文件，点击Branch，在输入框输入新的分支名称Hexo后会出现保存选项，保存新的分支，并将新的分支设置为默认分支。
## 建立Hexo站点

    hexo init HexoBlog
建立Hexo站点，设置站点相关内容，添加博客文章。
## 将站点内容提交到Hexo分支
在Git Bash窗口执行

将Hexo站点创建本地Git库

    git init

添加文件

    git add .

提交

    git commit -m "Hexo Blog add"

创建分支Hexo

    git branch Hexo

切换到分支Hexo

    git checkout Hexo

添加远程仓库

    git remote add origin git@github.com:xxx/xxx.github.io.git

拉取远程仓库

    git pull origin Hexo

推送Hexo站点到Hexo分支

    git push origin Hexo

在Github上有master和Hexo两个分支，其中Hexo分支中包含Hexo站点的原始文件，如果要切换工作环境，把Hexo分支签出即可。
## 部署Hexo站点
在Git Bash窗口执行

    hexo d
Hexo会根据deploy的设置，将静态博客部署到Github master分支。
## 全新环境恢复Hexo站点
签出Github上的Hexo分支。
用hexo init命令重新创建一个空的Hexo站点，将签出的Hexo分支的内容复制到新创建的Hexo站点，添加新的博客文章，利用hexo g生成，hexo d发布。