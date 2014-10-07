---
layout: post
title: 优先级队列
date: 2011-08-28 10:47
author: Little Horse
comments: true
categories: [技术, 算法, 《算法导论》笔记, 算法, 编程]
---
<span style="color: blue;"><strong>优先级队列</strong></span>（priority queue）是堆的一个常见应用。有两种队列：最大优先级队列和最小优先级队列。

优先级队列是一种用来维护由一组元素构成的集合S的数据结构，这一组元素中的每一个都有一个关键字key。
一个最大优先级队列 支持以下操作：

INSERT(S,x)：把元素插入集合S；

MAXIMUM(S):返回S中具有最大关键字的元素；

EXTRACT-MAX(S):去掉并返回S中具有的最大关键字的元素；

INCREASE-KEY(S,x,k)：将元素x的关键字的值增加到k，这里k值不能小于x的原关键字的值。

最大优先级队列的一个应用：分式计算机上进行作业调度。

最小优先级队列支持的操作包括：INSERT,MINIMUM,EXTRACT-MIN和DECREASE-KEY。

最小优先级队列的一个应用：用在基于事件驱动的模拟器中。

下面是最大优先级队列的具体操作：

<!--more-->

<strong>MAXIMUM(S)</strong>

[code lang="java"]public static int maximum(){
		return A[0];
	}[/code]

直接返回队列最大关键字，时间复杂度O(1)。

<strong>EXTRACT-MAX(S)</strong>

[code lang="java"]public static int extractMax(){
		if(heapSize &lt; 0){
			System.out.println(&quot;heap underflow&quot;);
		}
		int max = A[0];
		A[0] = A[heapSize - 1];
		heapSize--;
		maxHeapify(0, heapSize);
		return max;
	}[/code]

除少量固定工作外，调用maxHeapify函数，时间复杂度为O(nlgn)。

<strong>INCREASE-KEY(S,x,k)</strong>

[code lang="java"]public static void heapIncreaseKey(int i, int key){
		if(key &lt; A[i]){
			System.out.println(&quot;new key is smaller than current key&quot;);
		}
		A[i] = key;
		int parent = parent(i);
		while(i &gt; 0 &amp;&amp; A[parent] &lt; A[i]){
			int temp = A[i];
			A[i] = A[parent];
			A[parent] = temp;
			i = parent;
			parent = parent(i);
		}
	}[/code]

INCREASE-KEY过程将要更新的元素值更新为新值，然后将更新的节点不断向其父节点移动，直到满足最大堆性质。时间复杂度为O(lgn)。

<strong>INSERT(S,x)</strong>

[code lang="java"]public static void insert(int key){
		heapSize++;
		int[] B = new int[A.length + 1];
		System.out.println();
		for(int j = 0; j &lt; A.length; j++){
			B[j] = A[j];
		}
		A = B;
		A[heapSize - 1] = Integer.MIN_VALUE;
		heapIncreaseKey(heapSize - 1, key);
	}[/code]

INSERT过程首先在堆尾增加一个关键字值为负无穷的叶节点，然后调用INCREASE-KEY将值改为正确值。时间复杂度为O(lgn)。

<strong>测试代码：</strong>

[code lang="java"]public class PriorityQueue extends HeapSort{
	private static int heapSize = A.length;
        public static void main(String[] args){
		buildMaxHeap();
		for(int i : A){
			System.out.print(i + &quot;,&quot;);
		}
		System.out.print(&quot;\n&quot;);
		System.out.println(&quot;Max: &quot; + maximum());
		heapIncreaseKey(6, 8);
		System.out.println(&quot;Increase key: &quot;);
		for(int i : A){
			System.out.print(i + &quot;,&quot;);
		}
		insert(12);
		System.out.println(&quot;Insert key: &quot;);
		for(int i : A){
			System.out.print(i + &quot;,&quot;);
		}
	}
}[/code]
