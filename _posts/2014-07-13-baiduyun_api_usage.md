---
layout: post
title: 百度云API服务使用方法
date: 2014-07-13 22:50
author: Little Horse
comments: true
categories: [技术]
---
想写个小程序，需要访问百度云API，为此了解了它的使用方法，使用步骤记录如下。
<h2>1.注册应用</h2>
百度开放云（<a href="http://developer.baidu.com/">http://developer.baidu.com/</a>） ——开发者服务管理——创建工程，获得API Key。
<h2>2.用户授权获得Access Token</h2>
Oauth文档参见<a href="http://developer.baidu.com/wiki/index.php?title=docs/oauth">http://developer.baidu.com/wiki/index.php?title=docs/oauth</a>。

Access Token是用户授权后，获得的用来证明应用身份的字符串（我的理解），后面程序调用API时需要传入Access Token以证明自己的身份。

引导用户访问 <a href="https://openapi.baidu.com/oauth/2.0/authorize?response_type=token&amp;client_id=API_KEY&amp;redirect_uri=oob&amp;scope=netdisk">https://openapi.baidu.com/oauth/2.0/authorize?response_type=token&amp;client_id=API_KEY&amp;redirect_uri=oob&amp;scope=netdisk</a> ，把API_KEY换成上一步中获得的API KEY。

用户授权后跳转到页面<a href="http://openapi.baidu.com/oauth/2.0/login_success#expires_in=2592000&amp; access_token=ACCESS_TOKEN&amp;session_secret=SESSION_SECRET &amp;session_key=SESSION_KEY&amp;scope=basic+netdisk">http://openapi.baidu.com/oauth/2.0/login_success#expires_in=2592000&amp; access_token=ACCESS_TOKEN&amp;session_secret=SESSION_SECRET &amp;session_key=SESSION_KEY&amp;scope=basic+netdisk</a> ，把其中获得的Access Token保存下来，后面的API请求需要作为参数。
<h2>3. 访问百度云API</h2>
参考API列表，例如<a href="http://developer.baidu.com/wiki/index.php?title=docs/oauth/rest/file_data_apis_list#.E8.8E.B7.E5.8F.96.E5.BD.93.E5.89.8D.E7.99.BB.E5.BD.95.E7.94.A8.E6.88.B7.E7.9A.84.E7.AE.80.E5.8D.95.E4.BF.A1.E6.81.AF">获取当前登录用户的信息</a>，访问API的python代码为：

<img alt="" src="http://manan.org/images/wp/2014/07/clip_image001.png" />

运行程序，得到JSON格式的结果（示例）：
[code lang="js"] 
{
  &quot;uid&quot;:2346677,
  &quot;uname&quot;:&quot;liupc24&quot;,
  &quot;portrait&quot;:&quot;e2c1776c31393837313031319605&quot;
}
 [/code]
注意：我开始用家里的笔记本联网运行，出现socket错误信息，把脚本放在VPS上运行，结果正确。估计是家里网络的ip地址太多人共用，被百度服务器ban掉了。所以平时有个VPS备用还是很重要的。
