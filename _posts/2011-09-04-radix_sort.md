---
layout: post
title: 基数排序
date: 2011-09-04 19:24
author: Little Horse
comments: true
categories: [技术, 算法, 《算法导论》笔记, 算法, 编程]
---
<span style="color: blue;"><strong>基数排序（radix sort）</strong></span>从最低位到最高位依次对数字的每一位进行排序，待最高位排序结束后，整个数字的排序也完成了。对于按位排序算法，需要保证排序是稳定的，否则基数排序会出错。下面的实现中按位排序使用<a href="http://manan.org/archives/592" target="_blank">计数排序</a>。

<span style="color: blue;"><strong>Java程序实现 </strong>
</span>

[code lang="java"]public class RadixSort{
	public static void countingSortByDigit(int[]A, int[]B, int k, int digit){
		int[] C = new int[k + 1];
		for(int i : C){
			C[i] = 0;
		}
		int digitNum;
		for(int j = 0; j &lt; A.length; j++){
			//取数字的相应位数字用于排序
			digitNum = A[j] / (int)Math.pow(10, digit) % 10;
			C[digitNum]++;
		}
		for(int i = 1; i &lt;= k; i++){
			C[i] = C[i] + C[i - 1];
		}
		for(int j = A.length - 1; j &gt;= 0; j--){
			digitNum = A[j] / (int)Math.pow(10, digit) % 10;
			B[C[digitNum] - 1] = A[j];
			C[digitNum]--;
		}
	}

	public static int[] radixSort(int[]A, int d){
		for(int i = 0; i &lt; d; i++){
			int[] B = new int[A.length];
			countingSortByDigit(A, B, 9, i);
			A = B;
		}
		return A;
	}

	public static void main(String[] args){
		int[] A = {329, 457, 657, 839, 436, 720, 355};
		for(int i : A){
			System.out.print(i + &quot;,&quot;);
		}
		System.out.print(&quot;\n&quot;);
		A = radixSort(A, 3);
		for(int i : A){
			System.out.print(i + &quot;,&quot;);
		}
	}
}[/code]


<span style="color: blue;"><strong>算法复杂度</strong><span style="font-family: 宋体;">
</span></span>

给定n个d位数，每一个数位可以取k种可能的值。如果所用的稳定排序需要$$\Theta(n+k)$$的时间，基数排序能以$$\Theta(d(n+k))$$的时间正确地对这些数进行排序。当d为常数、$$k=O(n)$$时，基数排序具有线性运行时间。

<span style="color: blue;"><strong>练习题8.3-4</strong>
</span>

说明如何在O(n)时间内，对0到$$n^2-1$$之间的n个数进行排序。

Answer：将这n个数转换为基数为n的2位数，然后使用基数排序，则排序时间为$$\Theta(2(n))$$=$$\Theta(n)$$。
