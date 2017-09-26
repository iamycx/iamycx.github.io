---
layout: post
title:  Github+Jekyll半小时搭建个人网站
date:   2017-09-26 14:17:11 +08:00
category: 其他
tags: GitHub 搭建网站 安装
comments: true
---

* content
{:toc}

通过Github来搭建网站挺简单的，按顺序一步一步来就好，整个过程大概不超过一小时。








## 大致流程
1.注册Github
- 如果已经有账号了，就跳过这步

2.安装Git环境

3.SSH配置

4.建立个人Github Pages

5.写博客并同步到网站

6.本地安装
- Ruby和DevKit
- Jekyll


## 安装Git环境
- Windows7下安装Git

 [Git下载]( https://git-for-windows.github.io/)

安装好了之后在开始菜单中找到Git Bash并打开

![image.png](http://upload-images.jianshu.io/upload_images/3688263-a293ada2a07e2cf7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

再打开的 Git Bash 窗口中执行如下命令，设置Git用户名和邮箱：

```
$ git config -- global user.name "{username}" // 用你的用户名替换{username}  
$ git config -- global user.email "{name@site.com}" // 用你的邮箱替换{name@site.com}
```


## SSH配置
为了与Github的远程仓库传输，我们需要进行SSH加密设置
在刚才的 Git Bash 窗口执行
```
$ ssh-keygen -t rsa -C "{name @site .com}"    // 用你的邮箱替换{name @site .com}
```
一直敲回车直到命令完成，此时在用户目录下（Windows7系统目录  C:\Users\你的计算机用户名 ）出现了一个`.ssh`文件夹，此文件夹中有`id_rsa`和`id_rsa.pub`两个文件。打开`id_rsa.pub`文件，并复制全部内容。
打开Github网页，并登录后，点击右上角的头像，点击Settings

![image.png](http://upload-images.jianshu.io/upload_images/3688263-b9f207dfc9b17370.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

 点击SSH and GPG keys，点击New SSH key，在Key中粘贴`id_rsa.pub`文件全部内容，点Add SSH key。

![image.png](http://upload-images.jianshu.io/upload_images/3688263-0950f7a4102eb6f8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##  建立个人Github Pages


建立基于Jekyll的个人Github Pages有两条路线：

- 1.自己学习Jekyll教程和网页设计，设计自己的网页。
- 2.Fork（ Git系统的创建分支，简单来说是把当前仓库复制一份到你的仓库，你可以进行修改，因为你的仓库是原来仓库的新的分支 ）已有的开源博客仓库，在巨人的肩膀上进行符合自我的创作。


建议小白们可以从第二条路线学起。

直接Fork[主题]( https://github.com/iamycx/iamycx.github.io )到自己的仓库，点击Settings

![image.png](http://upload-images.jianshu.io/upload_images/3688263-71e99489d7710dbc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](http://upload-images.jianshu.io/upload_images/3688263-71130aede30c2021.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

 重命名为username.github.io 用你的用户名替代username， 此时你会发现已经可以通过`http://{你的Github用户名}.github.io `访问你Fork下来的网站啦！






##  写博客并同步到网站


- clone仓库

打开Git Bash， 输入以下命令切换到你想放置本地代码仓库的位置：

```
$ cd {本地路径}     // 比如： cd e:/workspace
```

clone（克隆）你自己的远程仓库：

```
$ git clone https: //github.com/{username}/{username}.github.io.git   // 用你的Github用户名替换{username}
```

![image.png](http://upload-images.jianshu.io/upload_images/3688263-3c97cd38e7897320.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

这时所有远程仓库里的源码都拷贝到`E:/Repositories/{username}.github.io`这个文件夹里来了。


- 写文章


打开本地仓库的`_posts`文件夹，你的所有博文都将放在这里，写新博文只需要新建一个标准文件名的文件，在文件中编写文章内容。 比如我们fork的模版中`_posts` 文件夹里有一篇 `2016-03-23-hello-world.markdown` ，你的文件命名也要严格遵循 `年-月-日-文章标题.文档格式` 这样的格式，尤其要注意`月份和日期一定是两位数`。 

推荐使用Markdown语言写文章，windows下推荐为知笔记这个软件编写Markdown文本。

- 上传文章到网站

>*  这里只介绍快速修改上传博客的方法，详细的Git学习可以参考文末给出的扩展阅读。



当你使用Git Bash对你的本地仓库进行操作时，先用  cd  命令将你的工作目录设置到你要操作的本地仓库

```
$ cd {你刚才 clone 下来的项目文件夹路径}
```

每当你对本地仓库里的文件进行了修改，只需在Bash中依次执行以下三个命令即可将修改同步到Github，刷新网站页面就能看到修改后的网页：

```
$ git add . $ git commit -m "statement" //此处statement填写此次提交修改的内容，作为日后查阅 $ git push origin master
```

到此你已经可以发表文章到你的个人博客啦！


##  安装Jekyll
- 安装 Ruby和DevKit，[参考]( https://jingyan.baidu.com/article/48b558e33558ac7f38c09aee.html )
- 安装Jekyll，[参考]( https://jingyan.baidu.com/article/925f8cb8f6422ac0dde056ee.html )
- 开启本地实时预览

上一小节的安装都完成以后，在 Git Bash 中输入命令

```
$ cd { local repository} // { local repository}替换成你的本地仓库的目录 $ jekyll serve
```
如果一路下来都没错误的话，通过在浏览器地址栏输入`http://localhost:4000/ `回车就已经可以看到自己网站的模样啦。


只要`jekyll serve`服务开着，你的本地仓库文件有任何更新，本地网站刷新都能马上看到，ok！





## 参考


>* [GitHub Help](https://help.github.com/categories/github-pages-basics/)
>* [GitHub Pages]( https://pages.github.com/)
>* [Jekyll](http://jekyllrb.com/)*（附上[中文版](http://jekyllcn.com/))*
