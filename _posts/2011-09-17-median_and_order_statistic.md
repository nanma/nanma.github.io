---
layout: post
title: 中位数和顺序统计学
date: 2011-09-17 14:59
author: Little Horse
comments: true
categories: [技术, 算法, 《算法导论》笔记, 算法, 编程]
---
<p>在一个由n个元素组成的集合中，第i个顺序统计量是该集合中第i小的元素。
</p><p>一个中位数是它所在集合的"中点元素"。当n为奇数，中位数出现在i=(n+1)/2处；当n为偶数，存在两个中位数，i=n/2和i=n/2+1。如果不考虑奇偶性，中位数出现在$$\lfloor(n+1)/2\rfloor$$处（下中位数）和$$\lceil(n+1)/2\rceil$$处（上中位数）。
</p><p>形式化地定义选择问题：
</p><p>输入：一个包含n个（不同的）数的集合A和一个数i，$$1\le i\le n$$。
</p><p>输出：元素$$x\in A$$，它恰大于A中其他的i-1个元素。
</p><p><span style="color:blue"><strong>最小值和最大值</strong>
		</span></p><p>在一个有n个元素的集合中，要通过n-1次比较才能找到最小值或最大值。
</p><p>如果同时找出最小值和最大值，则可以成对的处理元素，将一对输入元素进行比较，将较小者与当前最小值进行比较，将较大者与当前最大值进行比较，即每两个元素需要3次比较。这种情况下需要的比较次数是$$3\lfloor n/2\rfloor$$处（下中位数）
</p><p><span style="color:blue"><strong>一般选择问题</strong>
		</span></p><p>一般选择问题和找最小值的运行时间是相同的，都是$$\Theta(n)$$。基于快速排序算法的RANDOMIZED-SELECT算法，对输入数组进行递归划分，然后处理划分的一边。
</p><p><span style="color:blue"><strong>RANDOMIZED-SELECT Java实现
</strong></span></p>
[code lang="java"]public class RandomizedSelect{
	public static int randomizedPartition(int[] A, int p, int r){
		int s = (int)Math.ceil(Math.random() * (r - p)) + p;
		int temp = A[r];
		A[r] = A[s];
		A[s] = temp;
		int x = A[r];
		int i = p - 1;
		for(int j = p; j &lt; r; j++){
			if(A[j] &lt;= x){
				i++;
				temp = A[j];
				A[j] = A[i];
				A[i] = temp;
			}
		}
		i++;
		A[r] = A[i];
		A[i] = x;
		return i;
	}
	
	public static int randomizedSelect(int[] A, int p, int r, int i){
		if(p == r){
			return A[p];
		}
		int q = randomizedPartition(A, p, r);
		int k = q - p + 1;
		if(i == k){
			return A[q];
		} else if(i &lt; k){
			return randomizedSelect(A, p, q - 1, i);
		} else{
			return randomizedSelect(A, q + 1, r, i - k);
		}
	}
	
	public static void main(String[] args){
		int[] array = {3, 2, 6, 1, 9, 7, 8, 5, 4};
		for(int i : array){
			System.out.print(i + &quot;,&quot;);
		}
		System.out.print(&quot;\n&quot;);
		System.out.println(&quot;The i-th number:&quot; + randomizedSelect(array, 0, array.length - 1, 5));
	}
}
[/code]
<p><span style="color:blue"><strong>算法复杂度</strong><span style="font-family:宋体">
			</span></span></p><p>在最坏情况下，每次划分过程中都按照余下的元素中最大的进行划分，则运行时间为$$\Theta(n^2)$$。在平均情况下，运行时间为$$\Theta(n)$$。即平均情况下，任何顺序统计量都可以在线性时间内得到。
</p><p><span style="font-size:10pt"> 
</span> </p>
