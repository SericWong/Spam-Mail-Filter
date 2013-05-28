[ 博客网址 ]

	http://blog.csdn.net/rk2900/article/details/8984276
	
[ 总体思想 ]

	利用Naive Bayes（后验概率）计算特征所属空间的概率，取其最大者为判定结果。
	如下，其中P表示概率，w表示所属类别。

	对于Prior，可用如下公式进行计算：
	对于Likelihood中独立同分布的各项概率，可用如下公式计算：

[ 训练 ]

	输入为上万封电子邮件内容，包含垃圾邮件/非垃圾邮件。提取邮件内单词，改写为小写单词输入字典，过滤出现1次的单词，过滤长度只有1的单词，过滤出现总次数超过1万次的单词，最后形成我们的统计词典以及垃圾/非垃圾邮件词典。

[ 预测 ]

	定义probSPAM = probHAM = 1
	输入一封邮件，抽取其单词，对上述词典中的每一个单词进行处理：
	1）在垃圾邮件词典中，若单词A出现在当前邮件中，那么probSPAM *= （垃圾邮件中该单词出现次数）/（垃圾邮件数量）；
	2）在垃圾邮件词典中，若单词A没有出现在当前邮件中，那么probSPAM *= [1-（垃圾邮件中该单词出现次数）/（垃圾邮件数量）]；
	3）在非垃圾邮件词典中，若单词A出现在当前邮件中，那么probHAM *= （正常邮件中该单词出现次数）/（正常邮件数量）；
	4）在非垃圾邮件词典中，若单词A没有出现在当前邮件中，那么probHAM *= [1-（正常邮件中该单词出现次数）/（正常邮件数量）]；

	完成统计后，两个prob变量分别乘以（对应类别的邮件数）/（所有邮件总数），即 Prior。
	比较probSPAM以及probHAM，哪个相对较大就判定为对应空间。

[ 实现 ]

	用Python代码实现。


