---
layout: post
title: 快速排序
date: 2011-08-28 22:13
author: Little Horse
comments: true
categories: [技术, 算法, 《算法导论》笔记, 算法, 编程]
---
<strong><span style="color: #0000ff;">快速排序</span></strong>是一种排序算法，对包含n个数的输入数组，最坏情况运行时间为O(n^2)，平均运行时间为O(nlgn)，可以进行就地排序。快速排序通常是用于排序的最佳的使用选择。

和合并排序一样，快速排序也是基于分治模式，对一个典型子数组A[p..r]排序的分治过程包含三个步骤：

<span style="color: #0000ff;">分解</span>：将数组A[p..r]分成两个（可能空）的子数组A[p..q-1]和A[q+1..r]，使得A[p..q-1]中的每个元素都小于等于A[q]，而且小于等于A[q+1..r]中的元素。下标q在这个过程中计算。

<span style="color: #0000ff;">解决</span>：递归调用快速排序，对子数组A[p..q-1]和A[q+1..r]排序。

<span style="color: #0000ff;">合并</span>：整个数组A[p..r]已经排序。

<strong>数组划分PARTITION</strong>

快速排序算法的关键是数组划分过程PARTITION，它对子数组A[p..r]进行就地重排：

<!--more-->

[code lang="java"]public static int partition(int[] A, int p, int r){
        int x = A[r];
        int i = p - 1;
        for(int j = p; j &lt; r; j++){
            if(A[j] &lt;= x){
                i++;
                int temp = A[j];
                A[j] = A[i];
                A[i] = temp;
            }
        }
        i++;
        A[r] = A[i];
        A[i] = x;
        return i;
    }[/code]

PARTITION在子数组上的运行时间为O(n)，n=r-p+1。

<strong>快速排序实现</strong>

[code lang="java"]public static void quickSort(int[] A, int p, int r){
		if(p &lt; r){
			int q = partition(A, p, r);
			quickSort(A, p, q - 1);
			quickSort(A, q + 1, r);
			return;
		} else{
			return;
		}
	}[/code]

<strong>快速排序性能</strong>

快速排序的运行时间与划分是否对称有关。如果划分对称，快速排序从渐进意义上和合并算法一样快；如果划分不对称，快排和插入算法一样慢。

如果在算法的每一层递归上，划分都是最大程度不对称的，则运行时间是O(n^2)；如果每一层划分是最平衡的，则运行时间是O(nlgn)。在平均情况下，运行时间是O(nlgn)。

<strong>快速排序的随机化版本</strong>

对快速排序中加入随机化成分，使得对于所有输入，它均能获得较好的平均情况性能。

采用随机取样的方法，在子数组A[p..r]中随机选择一个元素和A[r]交换，再选取A[r]作为主元素，这样主元素是随机选择的。期望在平均情况下，对输入数组的划分能够比较匀称。

<strong>测试代码：</strong>

[code lang="java"]public class QuickSort{
public static void main(String[] args){
		int[] array = {3, 2, 6, 1, 9, 7, 8, 5, 4};
		for(int i : array){
			System.out.print(i + &quot;,&quot;);
		}
		System.out.print(&quot;\n&quot;);
		quickSort(array, 0, array.length - 1);
		for(int i : array){
			System.out.print(i + &quot;,&quot;);
		}
	}
}
	[/code]
