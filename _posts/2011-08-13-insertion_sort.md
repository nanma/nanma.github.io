---
layout: post
title: 插入排序
date: 2011-08-13 14:24
author: Little Horse
comments: true
categories: [技术, 算法, 《算法导论》笔记, 算法, 编程]
---
<span style="color: #0000ff;"><strong>插入排序</strong><span style="color: #000000;">（InsertionSort）</span></span>是一个对少量元素进行排序的有效算法，它的基本思想和打牌时整理牌的顺序方法类似：如果右手中有一组需要按照大小排序的牌，则依次从中取出一张牌放入左手，每次新取出的牌按照大小关系插入到左手牌中合适的位置，直到所有的牌都排序完成，因此称之为插入排序。

插入排序的Java代码如下所示：

<!--more-->

[code lang="java"]public class InsertionSort{
	public static int[] sort(int[] array){
		for(int i = 1; i &lt; array.length; i++){ 			                     
			int key = array[i]; 			                     
			int j = i - 1; 
			while(j &gt;= 0 &amp; array[j] &gt; key) {
		        array[j+1] = array[j];
				j--;
		    }
		    array[j+1] = key;
		}
		return array;
	}

	public static void main(String[] args){
		int[] array = {3, 2, 6, 1, 9, 7, 8, 5, 4};
		for(int i : array){
			System.out.print(i + &quot;,&quot;);
		}
		System.out.print(&quot;\n&quot;);
		array = sort(array);
		for(int i : array){
			System.out.print(i + &quot;,&quot;);
		}
	}
}[/code]

在最优情况下，即待排序数的顺序已经排好，则上面算法中，插入部分（while循环）不需要进行，插入排序的算法复杂度是O(n）；在最坏情况下，待排序数是逆序的，插入部分需要进行最多次，则算法复杂度是O(n^2）。

总结：插入排序对部分有序的数据是极好的排序算法，对小型数据也是较好的排序方法。
