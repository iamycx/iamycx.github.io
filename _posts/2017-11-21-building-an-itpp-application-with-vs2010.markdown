
---


layout: post
title: 在Visual Studio 2010环境下创建一个IT++应用程序
date:   2017-11-21 18:36:11 +08:00
category: 其他
tags: IT++ ITPP VS2010
comments: true
---


* content
{:toc}










上一篇讲到了在VS2010下安装IT++函数库，完成后就要涉及到怎么使用了。这里以64位WIN7为例。








- 下载[ t emplate Wizard ](http://herve.boeglen.free.fr/itpp_windows/chap2/itpp_matmex_template_2010.zip)， 解压后得到Express和VCWizards这两个文件夹。如果你64位系统，将他们拷到 C:\ProgramFiles (x86)\Microsoft Visual Studio 10.0\VC。 就是拷到VS2010的安装目录里面的VC子目录里面去，32位系统的也类似操作。会提示替换合并，全部点‘确定’。



- 将步骤一解压得到的 Express中的 VCProjects文件夹里面的所有文件复制到路径 C:\Program Files (x86)\Microsoft Visual Studio 10.0\VC\vcprojects 下，会有提示是否覆盖，全部选‘确定’。

- 打开VS2010， 新建工程，选择 VC++\Win32 项目，就可以看到 IT++ 选项了.新建一个IT++项目，并一直点确定。


  可以看到 IT++ 安装成功，但编译时不通过，关键是 IT++   需要和 SDK 进行连接，按照以下的步骤进行设置：



   右键点击你刚刚创建的项目，在配置属性->VC++目录，在包含目录下添加 C:\itpp-4.2 ,在库目录下添加 C:\itpp-4.2\lib 。


 



- 设置完毕。现在你可以新建一个IT++工程了，程序自带一个可以直接编译运行的程序，直接运行，ok啦。


- 参考
>* [ITPP Windows herve](http://herve.boeglen.free.fr/itpp_windows/chap2/chap2_2010.html )

