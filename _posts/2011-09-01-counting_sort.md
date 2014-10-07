---
layout: post
title: 计数排序
date: 2011-09-01 22:10
author: Little Horse
comments: true
categories: [技术, 算法, 《算法导论》笔记, 算法, 编程]
---
<span style="color: blue;"><strong>计数排序</strong></span>假设n个输入元素中的每一个都是介于0到k之间的整数，此处k为某个整数。当$$k=O(n)$$时，计数排序的运行时间为$$\Theta(n)$$。

计数排序的基本思想：对每一个输入元素x，确定出小于x的元素个数。根据这一信息把x直接放到最终输出数组的位置上。

假定输入是数组A[0..n-1]，length[A]=n。此外需要两个辅助数组：存放排序结果的数组B[0..n-1]，提供临时存储区的C[0..k]。（此处数组下标均从0开始，和《算法导论》伪代码描述不同。）

<span style="color: blue;"><strong>程序实现</strong>
</span>

[code lang="java"]
public class CountingSort{
	public static void sort(int[]A, int[]B, int k){
		int[] C = new int[k + 1];
		for(int i : C){
			C[i] = 0;
		}
		for(int j = 0; j &lt; A.length; j++){
			C[A[j]]++;
		}
		for(int i = 1; i &lt;=k; i++){
			C[i] = C[i] + C[i - 1];
		}
		for(int j = A.length - 1; j &gt;= 0; j--){
			B[C[A[j]] - 1] = A[j];
			C[A[j]]--;
		}
	}
	public static void main(String[] args){
		int[] A = {2,5,3,0,2,3,0,3};
		int[] B = new int[A.length];
		int k = 5;

		for(int i : A){
			System.out.print(i + &quot;,&quot;);
		}
		System.out.print(&quot;\n&quot;);
		sort(A, B, k);
		for(int i : B){
			System.out.print(i + &quot;,&quot;);
		}
	}
}[/code]

排序过程实际是四个循环，前三个循环统计出小于等于每个输入元素的数字个数，最后一个循环根据这些个数将待排序的数依次放到新数组中合适的位置。<span style="font-family: 宋体;">
</span>

<span style="color: blue;">计数排序的一个重要性质</span>：稳定性，即具有相同值的元素在输出数组中的相对次序没有改变。当卫星数据随被排序的元素一起移动时，稳定性比较重要。
