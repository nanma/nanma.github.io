---
layout: post
title: 用Lucene模糊搜索和ExtJs ComboBox实现搜索建议词效果
date: 2011-11-19 23:09
author: Little Horse
comments: true
categories: [技术, 搜索, 编程]
---
<span style="font-family: 宋体;">在搜索引擎输入框中输入搜索词时，会实时得到搜索建议：</span>
<p style="text-align: center;"><a href="http://manan.org/images/wp/2011/11/search-suggestion.png"><img class="aligncenter" title="search-suggestion" src="http://manan.org/images/wp/2011/11/search-suggestion.png" alt="" width="415" height="299" /> </a></p>
<span style="font-family: 宋体;">这些建议词是从搜索引擎的搜索记录中按照一定算法挖掘出的高关联度短语。如果没有搜索记录，能不能实现相关搜索建议呢？本文介绍一个简单的处理方法，下面将分别说明如何得到相关建议词和前端的实现方式。
</span>

<span style="color: #366092;"><strong>1.<span style="font-family: 宋体;">相关词语的获取</span></strong>
</span>

<span style="font-family: 宋体;">最直观的相关词语是：两个词语（短语）之间具有一部分相同字，另一部分不同，它们之间相同的部分所占比例越高，则两个词语越相关。例如，在这种情况下"计算机"和"计算器"是相关的，"计算机"和"计算机网络"是相关的。如果有一个词典包含足够的词语，并且支持这种模糊的词语匹配方式，就可以实现词语建议。
</span>

Lucene<span style="font-family: 宋体;">专门提供了模糊查询</span>FuzzyQuery<span style="font-family: 宋体;">实现上述功能</span>[1]<span style="font-family: 宋体;">。它采用编辑距离算法计算两个字符串之间的相似度，编辑距离用来计算从一个字符串转换到另一个字符串所需的最少插入、删除和替换的字母个数。例如，"</span>three<span style="font-family: 宋体;">"和"</span>tree<span style="font-family: 宋体;">"之间的编辑距离为</span>1<span style="font-family: 宋体;">。使用</span>FuzzyQuery<span style="font-family: 宋体;">查询时，和查询词距离越小的词评分越高，在结果中排名越高。这样就可以通过模糊搜索获得词库中最相近的词语。
</span>

<span style="font-family: 宋体;">实际操作中，建立</span>Lucene<span style="font-family: 宋体;">索引时每个</span>document<span style="font-family: 宋体;">的索引域中只索引一个词，这样从返回的结果文档中可以直接取出该域中的词语。
</span>

《Lucene<span style="font-family: 宋体;">实战》中给出了下面的代码展示</span>FuzzyQuery<span style="font-family: 宋体;">的用法：
</span>

[code lang="java"] public void testFuzzy() throws Exception {    indexSingleFieldDocs(new Field[] { new Field(&quot;contents&quot;,
                                                 &quot;fuzzy&quot;,
                                                 Field.Store.YES,
                                                 Field.Index.ANALYZED),
                                       new Field(&quot;contents&quot;,
                                                 &quot;wuzzy&quot;,
                                                 Field.Store.YES,
                                                 Field.Index.ANALYZED)
                                     });

    IndexSearcher searcher = new IndexSearcher(directory);
    Query query = new FuzzyQuery(new Term(&quot;contents&quot;, &quot;wuzza&quot;));
    TopDocs matches = searcher.search(query, 10);
    assertEquals(&quot;both close enough&quot;, 2, matches.totalHits);

    assertTrue(&quot;wuzzy closer than fuzzy&quot;,
               matches.scoreDocs[0].score != matches.scoreDocs[1].score);

    Document doc = searcher.doc(matches.scoreDocs[0].doc);
    assertEquals(&quot;wuzza bear&quot;, &quot;wuzzy&quot;, doc.get(&quot;contents&quot;));
    searcher.close();

  }[/code]

<span style="font-family: 宋体;">虽然模糊搜索相比分析搜索</span>log<span style="font-family: 宋体;">不够智能、缺乏时效性，但是在面向特定领域、有现成领域词典的情况下，这种方式简单而有效。例如，对专利领域，国际专利分类（</span>IPC<span style="font-family: 宋体;">）的官方文件对整个技术领域做了全面的分类描述，里面出现的词语对专利方面的应用做输入建议会有不错的效果。
</span>

<span style="color: #366092;"><strong>2.<span style="font-family: 宋体;">前端效果实现</span></strong>
</span>

ExtJs<span style="font-family: 宋体;">中的下拉选择框组件</span>ComboBox<span style="font-family: 宋体;">可以实现输入时动态更新推荐词语列表的效果。
</span>

ComboBox<span style="font-family: 宋体;">的输入框右侧有一个下拉箭头（见下图），可以修改配置项使其不显示，模拟输入框的效果。
</span>
<p style="text-align: center;"><img class="aligncenter" src="http://manan.org/images/wp/2011/11/111911_1509_LuceneExt2.png" alt="" /><span style="font-family: 宋体; font-size: 12pt;">
</span></p>
<span style="font-family: 宋体;">一个配置示例如下所示，几个关键的配置项做了注释：
</span>

[code lang="javascript"]
var suggestionCombo = new Ext.form.ComboBox({
					hiddenName : 'cname',
					fieldLabel : '名称',
					triggerAction : 'all',
					store : suggestionCombostore,
					displayField : 'text',
					mode : 'local',
					forceSelection : false,
					minListWidth : 270,
					resizable : true,
					allowBlank : false,
					editable : true,     //允许输入
					enableKeyEvents:true, //允许键盘输入事件
					hideTrigger: true, //隐藏下拉箭头
					anchor : '100%'
				}); [/code]

<span style="font-family: 宋体;">为了根据用户输入动态更新列表内容，需要监听键盘输入事件，在每次输入一个字时发送当前输入内容到后端，后端获取相关词语后返回前端，重新展示。事件处理部分的代码为：
</span>

[code lang="javascript"]suggestionCombo.on('keyup',function(textField,e){
				//如果键盘输入不是方向键，则更新列表
				if(!e.isNavKeyPress()){
					textField.getStore().load({params:{inputText:textField.getRawValue()}});
				}
            });  [/code]

<span style="font-family: 宋体;">上面的textField.getRawValue()即获取当前的输入文本内容，用于后台查询建议词。
</span>

<span style="font-family: 宋体;">最终实现的效果如下图所示：
</span>
<p style="text-align: center;"><img class="aligncenter" src="http://manan.org/images/wp/2011/11/111911_1509_LuceneExt3.png" alt="" /><span style="font-family: 宋体; font-size: 12pt;">
</span></p>
<span style="font-family: 宋体;">如果能完善索引的领域词库，改善中文分词效果，可以得到更好的搜索建议词列表。
</span>

<span style="color: #366092; font-family: 宋体;"><strong>参考文献</strong>
</span>

[1] 《Lucene<span style="font-family: 宋体;">实战》（第二版），</span>P94<span style="font-family: 宋体;">
</span>

[2] extjs google suggest效果, <a href="http://wodar.iteye.com/blog/553067"><span style="color: blue; text-decoration: underline;">http://wodar.iteye.com/blog/553067</span></a>

[3] Ext.form.ComboBox实现google Suggestion效果, <a href="http://love4j.iteye.com/blog/516399"><span style="color: blue; text-decoration: underline;">http://love4j.iteye.com/blog/516399</span></a>
