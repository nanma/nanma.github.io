---
layout: post
title: visual studio中设置Tab键对应的空格数的方法
date: 2010-09-18 21:11
author: Little Horse
comments: true
categories: [技术, 软件, 软件]
---
        编程时的缩进是编码规范的重要方面，良好的缩进可以提高代码阅读的效率。因为不同的开发环境中Tab键对应的空格数不同，所以一般编码规范中强调缩进时不要使用Tab键，而是用4个空格。这样虽然保证了编码规范，但一定程度上降低了效率。为了解决这个问题，可以在编译器中设置Tab键对应的空格数，继续使用Tab键缩进。

        Visual Studio中设置Tab键对应空格数的方如下：

        依次选择：<strong>工具-〉选项 -〉文本编辑器-&gt;所有语言-&gt;制表符：</strong>

<strong>        </strong>如下图所示：
<p style="text-align: center;">
<p style="text-align: center;">

[caption id="attachment_53" align="aligncenter" width="604" caption="缩进设置示意"]<a href="http://manan.org/images/wp/2010/09/Indentation1.png"><img class="size-full wp-image-53  " title="Indentation" src="http://manan.org/images/wp/2010/09/Indentation1.png" alt="缩进设置示意" width="604" height="394" /></a>[/caption]

</p>
        注意，如果要使Tab键的设置应用到所有语言中，则选择所有语言，否则选择需要的语言即可，上图选择了C/C++。

        将<strong>“制表符大小”</strong>和<strong>“缩进大小”</strong>设置为4，选中<strong>“插入空格”</strong>，确定即可。<strong>        </strong>
