---
layout: post
title: 合并排序
date: 2011-08-14 20:47
author: Little Horse
comments: true
categories: [技术, 算法, 《算法导论》笔记, 算法, 编程]
---
<strong><span style="color: #0000ff;">合并排序</span></strong>（merge sort）是利用分治法（divede-and-conquer)进行排序的方法，即将一个较大问题分解为n个规模较小而结构相似的问题，分别处理这些子问题然后将结果合并。合并排序将待排序的元素分成两部分，对每部分进行合并排序后，将两个分别有序的字部分合并起来成为一个有序结果。

下面算法中，mergeSort（int[] A, int p, int r）对数组A[p, r]进行排序，将问题分解递归处理，当待排序元素分解为只有一个时视为已经排好序；merge(int[] A, int p, int q, int r)将排好序的两部分元素进行合并，把已经排好序的A[p, q]和A[q+1, r]合并成按序排列的A[p, r]。

<!--more-->

[code lang="java"]public class MergeSort{
	public static int[] merge(int[] A, int p, int q, int r){
		int n1 = q - p + 1;
		int n2 = r - q;
		int[] L = new int[n1 + 1];
		int[] R = new int[n2 + 1];
		for(int i = 0; i &lt; n1; i++){
			L[i] = A[p + i];
		}
		for(int j = 0; j &lt; n2; j++){
			R[j] = A[q + j + 1];
		}
		L[n1] = Integer.MAX_VALUE;
		R[n2] = Integer.MAX_VALUE;
		int i = 0, j = 0;
		for(int k = p; k &lt;= r; k++){
			if(L[i] &lt; R[j]){
				A[k] = L[i];
				i++;
			}else{
				A[k] = R[j];
				j++;
			}
		}
		return A;
	}

	public static int[] mergeSort(int[] A, int p, int r){
		if(p &gt;= r){
			return A;
		}
		else{
			//如果数据类型非整型，q要向下取整
			int q = (p + r) / 2;
			A = mergeSort(A, p, q);
			A = mergeSort(A, q + 1, r);
			A = merge(A, p, q, r);
			return A;
		}
	}

	public static void main(String[] args){
		int[] array = {3, 2, 6, 1, 9, 7, 8, 5, 4};
		for(int i : array){
			System.out.print(i + &quot;,&quot;);
		}
		System.out.print(&quot;\n&quot;);
		array = mergeSort(array, 0, array.length - 1);
		for(int i : array){
			System.out.print(i + &quot;,&quot;);
		}
	}
}
[/code]

利用递归式和递归树可以证明，合并排序的时间复杂度是O(nlgn)。（见《算法导论》P21）
<span style="font-family: 宋体;"> </span>
