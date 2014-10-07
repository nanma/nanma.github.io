---
layout: post
title: Lucene Demo中的编码问题
date: 2011-04-26 21:49
author: Little Horse
comments: true
categories: [技术, Java, 搜索, 编程]
---
<p>使用Lucene自带的示例程序lucene-demos-3.0.3.jar时，发现其中的索引程序IndexHTML.java索引一些网页时会报错：</p>
<p>Parse Aborted: Lexical error at line 63, column 16.</p>
<p>Encountered: &quot;\u987b&quot; (39035), after : &quot;&quot;</p>
<p>出错的地方都是HTML标签中Unicode编码的中文字符处。<br />
	<span style="font-family:宋体"> </span></p>
<p>经过一些搜索和试验，解决办法如下：</p>
<p>1. （见<a href="http://www.wenhq.com/article/view_448.html">http://www.wenhq.com/article/view_448.html</a> ）</p>
<p>第一：先下载一个javacc</p>
<p>第二：修改HtmlParser.jj文件的</p>
<pre lang="java">options { IGNORE_CASE = true; STATIC = false;} 为：
options { IGNORE_CASE = true; STATIC = false; UNICODE_INPUT=true;}
</pre>
<p>第三：运行javacc HtmlParser.jj</p>
<p>第四：把产生出来的java文件覆盖JavaCC HTML Parser 的源文件</p>
<p>除了修改HtmlParse.jj外，还做了如下两处修改：</p>
<p>2.（见<a href="http://blog.eood.cn/lucene%E5%A6%82%E4%BD%95%E7%B4%A2%E5%BC%95utf-8%E6%A0%BC%E5%BC%8F%E6%96%87%E4%BB%B6" target="_blank">http://blog.eood.cn/lucene%E5%A6%82%E4%BD%95%E7%B4%A2%E5%BC%95utf-8%E6%A0%BC%E5%BC%8F%E6%96%87%E4%BB%B6</a>）</p>
<p>在IndexHtml.java文件中，</p>
<pre lang="java">HTMLParser parser = new HTMLParser(fis);
改为：
HTMLParser parser = new HTMLParser(fis,&quot;utf-8&quot;);
</pre>
<p>3.修改HTMLParser.java。</p>
<pre lang="java">public Reader getReader() throws IOException {}中，
pipeIn = new InputStreamReader(pipeInStream, &quot;UTF-16BE&quot;);
pipeOut = new OutputStreamWriter(pipeOutStream, &quot;UTF-16BE&quot;);
将上面两行原来的编码都换为UTF-8。
</pre>
<p>完成上面的修改后，把java文件都编译为class文件，重新打包。</p>
<p>注意打包时，应该切换到/demo路径下，即此时在文件夹窗口可以看到的应该是org文件夹。</p>
<p>打包命令是：</p>
<pre lang="java">jar cvf lucene-demos-3.0.3.jar org</pre>
<p>完成上述修改后就可以使用新的jar包进行文件索引操作。</p>

