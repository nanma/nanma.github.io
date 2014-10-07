---
layout: post
title: 排序算法思维导图总结
date: 2011-09-25 10:11
author: Little Horse
comments: true
categories: [技术, 算法, 《算法导论》笔记, 算法, 编程]
---
常用的排序算法包括：
<ol>
	<li>冒泡排序</li>
	<li>插入排序</li>
	<li><a href="http://manan.org/2011/08/merge_sort/" target="_blank">合并排序</a></li>
	<li>堆排序</li>
	<li>快速排序</li>
	<li>计数排序</li>
	<li>基数排序</li>
	<li>桶排序</li>
</ol>
下面按照稳定性、复杂度、适用特点进行总结。

稳定性：具有相同值的元素在输出数组中的相对次序没有改变。当卫星数据随被排序的元素一起移动时，稳定性比较重要。

复杂度：时间复杂度和空间复杂度。

适用特点：算法需要根据具体条件进行选择。

<span style="color: blue;">1.排序算法分类，稳定性和时空复杂度[1]：
</span>

<img src="http://manan.org/images/wp/2011/09/092511_0211_1.png" alt="" /><span style="font-size: 12pt;">
</span>

<span style="color: blue;">2.适用特点[1-4]：<!--more--><span style="font-family: 宋体;">
</span></span>
<div>
<table style="border-collapse: collapse;" border="0"><colgroup> <col style="width: 92px;" /> <col style="width: 105px;" /> <col style="width: 390px;" /></colgroup>
<tbody valign="top">
<tr>
<td style="border: 1pt solid #a3a3a3; padding: 5px;"><span style="color: #595959;"> </span></td>
<td style="border-width: 1pt 1pt 1pt medium; border-style: solid solid solid none; border-color: #a3a3a3 #a3a3a3 #a3a3a3 -moz-use-text-color; padding: 5px;"><span style="color: #595959;"> </span></td>
<td style="border-width: 1pt 1pt 1pt medium; border-style: solid solid solid none; border-color: #a3a3a3 #a3a3a3 #a3a3a3 -moz-use-text-color; padding: 5px;">
<p style="text-align: center;">特点</p>
</td>
</tr>
<tr>
<td style="border-width: medium 1pt 1pt; border-style: none solid solid; border-color: -moz-use-text-color #a3a3a3 #a3a3a3; padding: 5px;">插入排序</td>
<td style="border-width: medium 1pt 1pt medium; border-style: none solid solid none; border-color: -moz-use-text-color #a3a3a3 #a3a3a3 -moz-use-text-color; padding: 5px;">直接插入排序</td>
<td style="border-width: medium 1pt 1pt medium; border-style: none solid solid none; border-color: -moz-use-text-color #a3a3a3 #a3a3a3 -moz-use-text-color; padding: 5px;">数据基本有序时，可以减少数据交换和移动次数，提高效率</td>
</tr>
<tr>
<td style="border-width: medium 1pt 1pt; border-style: none solid solid; border-color: -moz-use-text-color #a3a3a3 #a3a3a3; padding: 5px;"></td>
<td style="border-width: medium 1pt 1pt medium; border-style: none solid solid none; border-color: -moz-use-text-color #a3a3a3 #a3a3a3 -moz-use-text-color; padding: 5px;">希尔排序</td>
<td style="border-width: medium 1pt 1pt medium; border-style: none solid solid none; border-color: -moz-use-text-color #a3a3a3 #a3a3a3 -moz-use-text-color; padding: 5px;">简单，适用于小数据量情况</td>
</tr>
<tr>
<td style="border-width: medium 1pt 1pt; border-style: none solid solid; border-color: -moz-use-text-color #a3a3a3 #a3a3a3; padding: 5px;">交换排序</td>
<td style="border-width: medium 1pt 1pt medium; border-style: none solid solid none; border-color: -moz-use-text-color #a3a3a3 #a3a3a3 -moz-use-text-color; padding: 5px;">冒泡排序</td>
<td style="border-width: medium 1pt 1pt medium; border-style: none solid solid none; border-color: -moz-use-text-color #a3a3a3 #a3a3a3 -moz-use-text-color; padding: 5px;">实际使用中效率较低，对数据有序性非常敏感</td>
</tr>
<tr>
<td style="border-width: medium 1pt 1pt; border-style: none solid solid; border-color: -moz-use-text-color #a3a3a3 #a3a3a3; padding: 5px;"></td>
<td style="border-width: medium 1pt 1pt medium; border-style: none solid solid none; border-color: -moz-use-text-color #a3a3a3 #a3a3a3 -moz-use-text-color; padding: 5px;">快速排序</td>
<td style="border-width: medium 1pt 1pt medium; border-style: none solid solid none; border-color: -moz-use-text-color #a3a3a3 #a3a3a3 -moz-use-text-color; padding: 5px;">分治，自顶向下。理论上最好的方法，应用广泛; 如果数据量大而且数据全部放在内存中，那么快速排序是首选的排序方法[4]</td>
</tr>
<tr>
<td style="border-width: medium 1pt 1pt; border-style: none solid solid; border-color: -moz-use-text-color #a3a3a3 #a3a3a3; padding: 5px;">选择排序</td>
<td style="border-width: medium 1pt 1pt medium; border-style: none solid solid none; border-color: -moz-use-text-color #a3a3a3 #a3a3a3 -moz-use-text-color; padding: 5px;">简单选择排序</td>
<td style="border-width: medium 1pt 1pt medium; border-style: none solid solid none; border-color: -moz-use-text-color #a3a3a3 #a3a3a3 -moz-use-text-color; padding: 5px;">对有序性不敏感，交换次数少</td>
</tr>
<tr>
<td style="border-width: medium 1pt 1pt; border-style: none solid solid; border-color: -moz-use-text-color #a3a3a3 #a3a3a3; padding: 5px;"></td>
<td style="border-width: medium 1pt 1pt medium; border-style: none solid solid none; border-color: -moz-use-text-color #a3a3a3 #a3a3a3 -moz-use-text-color; padding: 5px;">堆排序</td>
<td style="border-width: medium 1pt 1pt medium; border-style: none solid solid none; border-color: -moz-use-text-color #a3a3a3 #a3a3a3 -moz-use-text-color; padding: 5px;">不需要递归，适合大数据量，可用来实现优先队列</td>
</tr>
<tr>
<td style="border-width: medium 1pt 1pt; border-style: none solid solid; border-color: -moz-use-text-color #a3a3a3 #a3a3a3; padding: 5px;">其他排序</td>
<td style="border-width: medium 1pt 1pt medium; border-style: none solid solid none; border-color: -moz-use-text-color #a3a3a3 #a3a3a3 -moz-use-text-color; padding: 5px;">合并排序</td>
<td style="border-width: medium 1pt 1pt medium; border-style: none solid solid none; border-color: -moz-use-text-color #a3a3a3 #a3a3a3 -moz-use-text-color; padding: 5px;">分治，自底向上。对有序性不敏感，需要辅助空间，<del>不适合大数据量；</del>在处理大量数据的排序时，它不要求被排序的数据全部在内存中，所以在数据大于内存的容纳能力时，合并排序能大显身手。合并排序最常用的地方是数据库管理系统（DBMS）[4]</td>
</tr>
<tr>
<td style="border-width: medium 1pt 1pt; border-style: none solid solid; border-color: -moz-use-text-color #a3a3a3 #a3a3a3; padding: 5px;">非基于比较</td>
<td style="border-width: medium 1pt 1pt medium; border-style: none solid solid none; border-color: -moz-use-text-color #a3a3a3 #a3a3a3 -moz-use-text-color; padding: 5px;">计数排序</td>
<td style="border-width: medium 1pt 1pt medium; border-style: none solid solid none; border-color: -moz-use-text-color #a3a3a3 #a3a3a3 -moz-use-text-color; padding: 5px;">数据范围需要不大</td>
</tr>
<tr>
<td style="border-width: medium 1pt 1pt; border-style: none solid solid; border-color: -moz-use-text-color #a3a3a3 #a3a3a3; padding: 5px;"></td>
<td style="border-width: medium 1pt 1pt medium; border-style: none solid solid none; border-color: -moz-use-text-color #a3a3a3 #a3a3a3 -moz-use-text-color; padding: 5px;">基数排序</td>
<td style="border-width: medium 1pt 1pt medium; border-style: none solid solid none; border-color: -moz-use-text-color #a3a3a3 #a3a3a3 -moz-use-text-color; padding: 5px;">关键字需要可分解</td>
</tr>
<tr>
<td style="border-width: medium 1pt 1pt; border-style: none solid solid; border-color: -moz-use-text-color #a3a3a3 #a3a3a3; padding: 5px;"></td>
<td style="border-width: medium 1pt 1pt medium; border-style: none solid solid none; border-color: -moz-use-text-color #a3a3a3 #a3a3a3 -moz-use-text-color; padding: 5px;">桶排序</td>
<td style="border-width: medium 1pt 1pt medium; border-style: none solid solid none; border-color: -moz-use-text-color #a3a3a3 #a3a3a3 -moz-use-text-color; padding: 5px;">数据分布均匀</td>
</tr>
</tbody>
</table>
</div>
<blockquote><span style="color: blue;"><span style="color: #000000;">在数据量不大时，所有排序算法性能差别不大。有文章指出，高级排序算法在元素个数多于1000 时，性能才出现显著提升。在90%的情况下，我们存储的元素个数只有几十到上百个而已，比如进程数、窗口个数和配置信息等等的数量都不会很大，冒泡排序其实是更好的选择。[4]</span>
</span></blockquote>
<span style="color: blue;">3.算法选择[3]</span>

<img src="http://manan.org/images/wp/2011/09/092511_0211_2.png" alt="" /><span style="font-family: 宋体; font-size: 12pt;">
</span>

最后推荐一个网站<a href="http://www.sorting-algorithms.com/">Sorting Algorithm Animations</a>，这里可以看到各种排序算法在不同数据条件下排序过程的动画演示，非常直观。

参考文献<span style="font-family: 宋体;">
</span>

[1]算法之排序算法,董的博客,http://dongxicheng.org/structure/sort/

[2]八种排序算法总结,http://blog.csdn.net/yfqvip/article/details/3344007

[3] 基本排序算法比较与选择,http://blog.csdn.net/ctang/article/details/37914

[4] 《系统程序员成长计划》
