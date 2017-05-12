# sorting-algorithm-notes

theory&amp;code implementation
#热门排序算法总结
	 
  最近将连续放出积压很久的一些笔记整理。本篇将主要简述热门排序算法具体应用的一些数理原理。
##威尔逊区间：
威尔逊区间是在1927年，美国数学家 Edwin Bidwell Wilson提出了一个修正公式，被称为"威尔逊区间 "，很好地解决了小样本的准确性问题。即无关时间取值的排名,即在少量样本和极端样本情况下的二项分布的置信区间计算具体实例是Reddit网站的排名算法便依赖于此。
原理：
借用对于一个话题的态度的支持和反对这个常见问题抽象为一个二项分布实际样本。那么对于这样的话题的热度排名可以转化为对于一个二项分布的置信区间的下界排序问题。（置信区间和事件发生概率要正确理解！）
最常见的二项分布的置信区间计算是用正态分布来进行计算的，然而这样的计算依赖于被测试样本的数量。因为，正态分布的计算置信区间是依赖于中心极限定理的，其公式是：
(1 )/n [n_(S )± z √(1/n n_S n_F )]
由于中心极限定理不适用于样本值小于30的情况，以及样本值趋近于0或1时的情况。
由此，一个重要理论推导产生，这个置信区间利用假设检验的反演，当总体参数的置信区间代表这些值如果他们测试假设的数量比例，θ值的集合可以表示为正常的近似是有效的表示为：（其中y是标准正态分布1/2α的分位点）
{Θ|y≤(p ̂-Θ)/√(1/n Θ(1-Θ) )≤z}
接下来我们直接上而威尔逊区间的表示，即如下两种表示方法：
1/(1+z^2/n) [n_S+z^2/2±z√(1/n n_S n_F+z^2/4)]
以及公式：
1/(1+z^2/n) [p ̂+z^2/2n±z√(1/n p ̂(1-p ̂ )+1/(4n^2 ) z^2 )]
其中：P ̂表示的是在N重伯努利试验中成功的比率，Z是1-1/2 α 与目标误差率对应的标准正态分布的数量（以α=95%为例，z=1.96），标准正态分布概率P，推导出该分布近似正态分布的标准差：√(1/n P(1-P) );由于该分布并不是二项分布，故P ̂和P的下边界之间将会有一个误差区间α，同理和P的上边界也有一个误差区间α。这样威尔逊区间利用皮尔斯卡方检测可以推导出它误差的范围，并可以利用之前正态分布中的假设公式表示即：
{Θ|y≤(p ̂-Θ)/√(1/n Θ(1-Θ) )≤z}
利用Θ以产生一个威尔逊区间，这个测试模型也可以作为一个得分测试。
威尔逊区间的置信均值表示为：(P ̂+Z^2/2n)/(1+1/n Z^2 )
在实际的排名运算中我们取威尔逊区间的下边界作为排序的标量以解决排序问题。著名网站Reddit的排名算法就是利用威尔逊区间下界作为排序标量完成的。 
参考资料：
维基百科：Binomial proportion confidence interval
（https://en.wikipedia.org/wiki/Binomial_proportion_confidence_interval）
阮一峰的博客：基于用户投票的排名算法（五）：威尔逊区间（http://www.ruanyifeng.com/blog/2012/03/ranking_algorithm_wilson_score_interval.html）；
How Not To Sort By Average Rating
（http://www.evanmiller.org/how-not-to-sort-by-average-rating.html）
