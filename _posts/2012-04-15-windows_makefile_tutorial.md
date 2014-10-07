---
layout: post
title: windows下使用makefile示例
date: 2012-04-15 23:26
author: Little Horse
comments: true
categories: [技术, 软件, 编程]
---
一、环境准备

1.安装MinGW
2.修改环境变量，把%MinGW%/bin添加到path中（%MinGW%为MinGW安装路径）
3.把%MinGW%/bin中的mingw32-make.exe复制，并重命名为make
验证上面三步是否成功：
在cmd窗口中输入，make -v，如果输出make版本信息则安装正确。

二、makefile测试
1.在准备测试的路径（如 C:\Users\James\test）下新建如下两个代码文件：
[code lang="c"]//---------------------------main.c : ---------------------------//
#include &quot;stdio.h&quot;
main()
{
    func();
    printf(&quot;this is main\n&quot;);
    getch();
}[/code]

[code lang="c"]//---------------------------func.c : ---------------------------//
#include &quot;stdio.h&quot;
func()
{
    printf(&quot;this is func\n&quot;);
    getch();
}[/code]

2.新建makefile文件：
[code lang="c"]
test:main.o func.o
    gcc -o test main.o func.o
func.o:func.c
    gcc -c func.c
main.o:main.c
    gcc -c main.c
[/code]

注意：上面的gcc -o和gcc -c前面必须是<strong>TAB</strong>，不是空格，否则运行make时会报错：“makefile:2: *** missing separator. Stop.”。

3.在cmd中切换至当前路径（C:\Users\James\test）下，运行make命令，输入： make 回车。
make命令执行的结果为：
[code lang="c"]C:\Users\James\test&gt;make
gcc -c main.c
gcc -c func.c
gcc -o test main.o func.o[/code]

此时路径下已经编译生成了test.exe，输入test即可看到运行结果。

本文主要参考了[1]，windows下的各版本gcc介绍可以参考[2]，makefile入门可以参考陈皓的《跟我一起写 Makefile》[3].

参考资料
[1]windows下使用makefile编译C语言: <a href="http://blog.csdn.net/zhanghan3/article/details/1334308">http://blog.csdn.net/zhanghan3/article/details/1334308</a>
[2]gcc for Windows开发环境介绍， <a href="http://blog.csdn.net/Mobidogs/article/details/1819084">http://blog.csdn.net/Mobidogs/article/details/1819084</a>
[3]跟我一起写 Makefile,<a href="http://blog.csdn.net/haoel/article/details/2886">http://blog.csdn.net/haoel/article/details/2886</a>
