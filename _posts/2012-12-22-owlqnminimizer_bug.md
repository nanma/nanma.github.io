---
layout: post
title: standford nlp包中OWLQNMinimizer的bug一则
date: 2012-12-22 05:21
author: Little Horse
comments: true
categories: [技术]
---
<div>Orthant-Wise Limited-memory Quasi-Newton(OWL-QN)算法的最初实现是<a href="http://research.microsoft.com/en-us/downloads/b1eb1016-1738-4bd5-83a9-370c9d498a03/">C++版本</a>，standford nlp包中曾经提供了该算法的java版本，后来由于授权问题不再提供该程序。目前可以<a href="http://224n-period-classifier.googlecode.com/svn/trunk/src/edu/stanford/nlp/optimization/OWLQNMinimizer.java">在这里</a>找到算法的java实现。</div>
<div>但是这个实现有bug，在OWLQNMinimizer.java中，LogisticRegressionProblem类中的Pair&lt;List&lt;Integer&gt;[], List&lt;Double&gt;[]&gt; readMatrixFile(String filename, boolean coordinate)方法用于读取Matrix Market Exchange Formats格式的矩阵文件，其中有两行代码用于计算矩阵元素的行列坐标：</div>
[code lang="java"]
int row = numNonZero / numFeats;
int col = numNonZero % numIns;[/code]
<div>由于Matrix Market Exchange Formats格式里，采用array方式输入矩阵时，矩阵元素是按列排列的，上面的计算错误。正确的代码是：</div>
[code lang="java"]
int row = numNonZero % numIns;
int col = numNonZero / numIns;
[/code]
<div>写出来意义不大，但是也许有人会遇到同样的问题，可以作为参考。</div>
</br>
Matrix Market Exchange Formats：
<a title="http://math.nist.gov/MatrixMarket/formats.html#MMformat " href="http://math.nist.gov/MatrixMarket/formats.html#MMformat " target="_blank"> http://math.nist.gov/MatrixMarket/formats.html#MMformat
</a><a title="http://people.sc.fsu.edu/~jburkardt/data/mm/mm.html" href="http://people.sc.fsu.edu/~jburkardt/data/mm/mm.html" target="_blank"> http://people.sc.fsu.edu/~jburkardt/data/mm/mm.html</a>
