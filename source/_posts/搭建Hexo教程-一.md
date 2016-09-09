---
title: 搭建Hexo教程(一)
date: 2016-09-09 15:47:42
tags: hexo
---
# 前言
好久之前就在试着搭建业内流传得很火的Hexo博客框架,今天趁着项目完工,闲着没事又把博客搭建起来了.

给出几个教程

[HEXO+Github,搭建属于自己的博客(简书)](http://www.jianshu.com/p/465830080ea9)

[Hexo搭建Github静态博客(博客园)](http://www.cnblogs.com/zhcncn/p/4097881.html)

### 1. 配置Hexo
安装 `git` 和 `node.js` 就不说了,直接找个盘新建一个文件夹,比如 `d:/hexo`,在该目录下右击 `Git Bash Here`

1. `npm install -g hexo` 通过npm全局安装hexo , 此命令容易Error , 请多试几次 , 实在不行就fq吧...
2. `hexo init` 初始化hexo
3. `npm install` 在当前目录安装npm
4. `hexo server` 启动hexo服务
5. 在浏览器输入 `localhost:4000`,如果能打开网页即成功构建hexo
6. 按 `ctrl+c` 关闭服务
7. 在 `github` 上新建一个 `repository` ,名字一定得是`用户名.github.io`, 完毕后将链接模式改为SSH, 原因后面会说
8. 新建SSH密钥, 执行 `ssh-keygen -t rsa -C “你的邮箱”`, 会让你输入名字,直接回车,然后输密码,也是回车
9. 打开 `c:/用户/用户名/.ssh/id_rsa.pub`, 复制里面的密钥
10. 打开 `github个人主页->Settings->SSH and GPG keys->New SSH Key` , `Title` 随意填写, `Key` 填写刚刚复制的密钥内容,然后`Add SSH key` 
11. 执行 `ssh -T git@github.com` , 检测SSH访问是否通畅, 如果结果是hi~xxxx,则表示SSH配置成功.
12. 修改目录下的 `_config.yml` 文件, 将deploy部分修改如下:
```
deploy:
  type: git
  repo: git@github.com:用户名/用户名.github.io.git
  branch: master
```
13. 执行 `hexo npm install hexo-deployer-git --save` 进行保存
14. `hexo clean`
15. `hexo g -d`
16. 在浏览器输入 `用户名.github.io` , 如果可以访问即表示部署成功

### 2. 修改主题

参考
[有哪些好看的Hexo主题?](http://www.zhihu.com/question/24422335)(知乎)  
具体的教程在主题的github上都有写

### 3. 如何发表文章?

1. 执行 `hexo new "你要写的文章的名字"`
2. 如果你还没有Markdown, 就赶紧下载这个超好用的轻量级文本编辑器吧 [点我下载Markdownpad](http://markdownpad.com/download.html)
3. 如果你是 win8 或者 win10 还需要下载 [Markdown Awesomium](http://markdownpad.com/download/awesomium_v1.6.6_sdk_win.exe)
4. 都安装完毕后就可以愉快的编辑 `.md` 格式的文件了

> **注**: 文章都放在hexo博客目录 `/source/_posts` 下  

### 4. Markdown语法?

参考 [Markdown 11种基本语法](http://www.cnblogs.com/hnrainll/p/3514637.html)

### 5. 为什么要使用SSH而非Https?

因为笔者在每次修改github库的时候都会提示输入我open SSH , 并让我输入用户名和密码 , 由于没有找到好的解决方法 , 所以我索性直接开启SSH模式 , 从此一切顺畅无碍.

### 6. 怎么删除文章 ?

1.  删除文章
2.  删除根目录下的db.json
3.  `hexo clean`
4.  `hexo g -d`