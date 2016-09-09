---
title: 搭建Hexo教程(二)
date: 2016-09-09 15:55:58
tags: hexo
---
### 前言
关于搭建Hexo的基础教程我已经写出来了 [搭建Hexo教程(一)](https://xswyt1543.github.io/2016/09/09/%E6%90%AD%E5%BB%BAHexo%E6%95%99%E7%A8%8B-%E4%B8%80/) , 可是如果有一天 get a new 笔记本 , 是否还要执行前面的教程呢 , 当然可以不 , 但要做出一些取舍.
  
* 如果你有这种需求(更换电脑), 就不要按 `教程一` 来搭建 , 请按照本文章来进行  
* 更新 / 提交博客的方式会更加麻烦  

#### 1. 怎么做 ?
先看看  
[使用hexo , 如果换了电脑怎么更新博客 ?](https://www.zhihu.com/question/21193762)  

当然 , 你也可以不看 ,直接看我写的就好了...(。・・)ノ 

***

*  需要建立 `2` 个分支 , 一个是默认的 `master` , 一个是 `hexo` , 新的分支的名字可以随便起~
*  新建一个文件夹 , 依次执行  
*  `git bash`  
*  `git clone 你的仓库的SSH地址` 
*  `git init`
*  新建分支 , 楼主在这踩了坑 , 网上说的那些 **新建branch** 的命令都不起作用 , 在看了大量教程之后 , 才发现正确做法是 `git checkout -b xxx` , `xxx` 是你要新建的分支的名字 , 而这条命令会自动 `新建` 分支并 `跳到` 这条分支上去 , 是不是很简单方便?
*  这个时候的分支应该是挂载在你的新分支上的 , 不过这还没完 , 到你的仓库去 , `branches -> change default branch -> 选择你的新分支 -> Update`
> 然而重点在后面(* "･∀･)ﾉ――◎

* 执行`npm install hexo`
* `hexo init`
* `npm install`
* 修改 `_config.yml` 文件 , 将 `branch` 配置为 `master` 分支 , `repo` 是仓库地址(ssh) , `type` 为 `git` , 还有主题 , 标题 , 介绍 等等
* 如果你还没有配置 `SSH` , 就去看看 [搭建Hexo教程一](https://xswyt1543.github.io/2016/09/09/%E6%90%AD%E5%BB%BAHexo%E6%95%99%E7%A8%8B-%E4%B8%80/) 把
* 执行 `npm install hexo-deployer-git --save`

> 请确认已切换到新分支 , 而非 `master` 分支

* 执行 `git add .`

> 这里有可能会出现 `file name too long` 的错误 , 解决方法是执行 `git config core.longpaths true` , 然后再执行 `git add .`

* `git commit -m "..."`
* `git push origin xxx` 通过 `xxx` 分支修改
* `hexo g -d` 通过 `matser` 分支修改

`create` 部分就到这里吧...

### 2. 每次更新提交要怎么做 ?

1. `git add .`
2. ` git commit -m "..."`
3.  `git push origin xxx`
4.   `hexo g -d`  

是不是感觉很麻烦 , 的确 ,可是不用再重新搭建Hexo , 还行吧...

> 如果只修改hexo的原始文件比如给主题添加一张照片等 ,只需要执行 `hexo g -d` ,如果你修改了 `_config.yml` , 你还要执行 `npm install hexo-deployer-git --save`

### 3. 重点: 在新的环境下怎么做?
1. 将仓库的内容 `clone` 下来
2. `git init`
3. `npm install hexo`
4. `npm install`
5. `npm install hexo-deployer-git`
> 切记,不要执行`hexo init`

### 4. 双分支的用意?

* `master` 分支拿来装生成的静态网页
* `xxx` 分支拿来装 `hexo` 搭建的原始文件
* 平时更新都在 `master` 分支
* 到了新环境只需要 `clone` `xxx` 分支即可.是不是很方便呢?

>对了 , 需要说明的是 `git` 操作是对当前的分支操作 , 而 `hexo` 是对 `_config.yml` 里面配置的 `branch` 操作的  
#### The end