---
layout: post
title:  Visual Studio 2010环境安装IT++函数库
date:   2017-11-21 18:34:11 +08:00
category: 其他
tags: IT++  安装 VS2010
comments: true
---


* content
{:toc}












听师兄说IT++库可以用来做ICA，google找了半天资料才装好，为了后来的同学们少走弯路，把安装过程记录下来。










#  [下载](https://sourceforge.net/projects/itpp/files/itpp/4.2.0/itpp-4.2.tar.bz2/download/) 并解压IT++ 4.2.0


解压出 名字为itpp-4.2的文件夹，里面是一些杂七杂八的东西，不用管它。将itpp- 4.2这个文件夹拷到C盘根目录中（不是必须，但建议这样，后面的步骤和这相关）。


# 在C:\itpp-4.2路径下创建文件夹lib


#   下载以下 这三个文件，并将它们放入新建的lib文件夹：


[ blas_win32.lib ]( http://herve.boeglen.free.fr/itpp_windows/chap1/blas_win32.lib )

[ lapack_win32 .lib ]( http://herve.boeglen.free.fr/itpp_windows/chap1/lapack_win32.lib )

[ libfftw3-3.lib ]( http://herve.boeglen.free.fr/itpp_windows/chap1/libfftw3-3.lib )



#   下载以下 这三个文件， 如果你是32位系统，就将这3个.dll文件放入             C:\windows\system32这个目录中，如果你是64位系统，就放入C:\windows\SysWOW64中 ：


[ blas_win32.dll ]( http://herve.boeglen.free.fr/itpp_windows/chap1/blas_win32.dll )

[ lapack_win32.dll ]( http://herve.boeglen.free.fr/itpp_windows/chap1/lapack_win32.dll )

[ libfftw3-3.dll ]( http://herve.boeglen.free.fr/itpp_windows/chap1/libfftw3-3.dll )


#   双击目录  c:\itpp-4.2\win32下的 itpp_mkl.sln ，这将会启动 VS2010，并 启动转换向导。一直点下一步，直至完成。




#   双击目录  c:\itpp-4.2\win32下的 itpp_mkl.sln ，打开后先别编译。按下面的图 改项目参数。 (项目/属性)


 
 

 
 
#   用VS2010打开路径 C:\itpp-4.2\itpp 下的头文件 config_msvc.h ，里面有3行

```
#if defined(HAVE_ACML) || defined(HAVE_MKL)

```
通过VS的查找功能找出这3行代码，将其替换为
```
#if defined(HAVE_ACML) || defined(HAVE_MKL) || defined(HAVE_FFTW3)    



```

记得保存一下。

打开 c: \itpp-4.2\itpp\signal\transforms.cpp ,找到48行，将其修改为
```
# include <itpp/fftw3.h>


```               

记得保存。





#   在 c: \itpp-4.2\itpp\ 目录下新建一个 fftw3.h 文件，并将  [ 网页 文件 ]( http://herve.boeglen.free.fr/itpp_windows/chap1/fftw3.h ) 复制到此 fftw3.h 文件 。

  打开 c: \itpp-4.2\itpp\signal\transforms.cpp ,找到48行，将其修改为

```

# include <itpp/fftw3.h>

```

保存一下。 #  打开 c:\itpp-4.2\win32下的 itpp_mkl.sln， 按F7即可编译了，完成后，会发现在我们刚刚新建的lib目录下会有 itpp_debug2010.lib 这个文件，大概60多MB.


# 修改属性文件

  打开 c:\itpp-4.2\win32下的 itpp_mkl.sln， 按F7再进行一次编译，完成后，会发现在我们刚刚新建的lib目录下会有 itpp_rel2010.lib 这个文件。会发现这次编译比上次快多了。




# 参考


>* [ITPP Windows herve](http://herve.boeglen.free.fr/itpp_windows/chap1/chap1_2010.html)
