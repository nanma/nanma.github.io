---
layout: post
title: ExtJS TreeGrid叶子节点拖拽问题和选择框使用方法
date: 2011-11-09 23:20
author: Little Horse
comments: true
categories: [技术, 编程]
---
最近一直参与开发一个实验室项目，接触到了ExtJs。下面是工程中几个小问题的总结。

1.TreeGrid的叶子节点拖拽问题

我使用的是ExtJs3.1版本。ExtJs中默认在树（Ext.tree.TreePanel）的拖动中，一个节点是不能拖动到一个叶子节点中的。这样的设计有些武断，因为根据应用环境叶子节点是有可能变为父节点的。事件机制给这个问题带来了解决方案，许多地方都提到了在监听TreePanel的"nodedragover"事件时特殊处理使得叶子节点可以被drop。代码为：

[code lang="javascript"]tree.on(&quot;nodedragover&quot;, function(e){
        var n = e.target;
        if (n.leaf) {
            n.leaf = false;
        }
        return true;
    });
[/code]

最后的返回值设为true使得目标叶子节点接受拖动的节点。

在使用TreeGrid（Ext.ux.tree.TreeGrid）时，同样面临上面的问题。采取同样的处理方式，尽管TreeGrid是继承自TreePanel，却仍不能使叶子节点被drop：

<img src="http://manan.org/images/wp/2011/11/110911_1520_ExtJSTreeGr1.png" alt="" /><span style="font-size: 12pt;">
</span>

在上面的事件处理函数中加打印语句，发现在TreeGrid有叶子节点被drop时，nodedragover事件根本就没有被触发。

试着调试一下，把页面引入的ext-all.js换成ext-all-debug.js，从触发nodedragover的地方入手逐渐分析，最终发现当TreePanel的拖拽配置为dropConfig: {appendOnly:true}时，nodedragover是不会触发的。这里TreePanel和TreeGrid的区别是，TreePanel如果不设置dropConfig属性，默认appendOnly是false；而TreeGrid如果不设置dropConfig属性，默认appendOnly是true。所以同样的处理到了TreeGrid这里就无效了。

明白了原因，只需要在TreeGrid的配置项里增加：dropConfig: {appendOnly:false}和上面的nodedragover事件处理函数就能实现TreeGrid的叶子节点drop问题，效果如下：

<img src="http://manan.org/images/wp/2011/11/110911_1520_ExtJSTreeGr2.png" alt="" /><span style="font-size: 12pt;">
</span>

2.TreeGrid中增加选择框（checkBox）效果

TreePanel没有直接提供checkBox的配置项，官方例子中的处理完全可以用在TreeGrid上，见/examples/tree/check-tree.html，主要是在数据中增加"checked: false"字段，然后用treeGrid.getChecked()方法获得当前选中的所有节点。效果如下：

<img src="http://manan.org/images/wp/2011/11/110911_1520_ExtJSTreeGr3.png" alt="" /><span style="font-size: 12pt;">
</span>

小结：初步尝试了前端开发动作，感觉设计某项功能具体的实现方式、界面的样式特别是交互方式，是很有乐趣的工作。
