# Decision Tree
决策树可以理解为一种多维的更复杂的Step Function。
其变化是顺便而非平滑。
作为一种可解释的预测模型，决策树也分为分类树和回归树
树的节点
	Internal Node
		组成：Features和Values
		Features是一个d维向量，维度的下标为j
		Split Values拆分值，一个数
		左子节点是条件维度小于Split Value，右子节点是条件维度大于等于Split Value。
	Leaf Node
		在给定触发条件下返回的预测（输出）值
	![[决策树结构示意举例.png]]
# Growing a Decision Tree
给出一个数据集$I$，给出分类机制来把$I$中的Label分类，并形成一个决策树。
基于树的结构，我们要调用递归函数。
BuildTree($I$，$k$)
	如果$|I|<k$
		记$\widehat{y}=average_{i\in I}y^{(i)}$
		返回一个叶子节点 Leaf(label = $\widehat{y}$) 这里的label是基于树的预测值
	否则
		对于Feature的每一个维度 $j$ 和所有点中的一个在这个维度下的坐标$s$
			设子集$I^+_{j,s}=\begin{Bmatrix} i\in I|x^{(i)}_j \geq s \end{Bmatrix}$
			设子集$I^-_{j,s}=\begin{Bmatrix} i\in I|x^{(i)}_j < s \end{Bmatrix}$
			设平均值$\widehat{y}^+_{j,s}=average_{i\in I^+_{j,s}}y^{(i)}$
			设平均值$\widehat{y}^-_{j,s}=average_{i\in I^-_{j,s}}y^{(i)}$
			设误差（损失）$E_{j,s}=\sum_{i\in I^+_{j,s}}(y^{(i)}-\widehat{y}^+_{j,s})^2+\sum_{i\in I^-_{j,s}}(y^{(i)}-\widehat{y}^-_{j,s})^2$
		设 $(j^*,s^*)=argmin_{j,s}E_{j,s}$
		返回一个Internal节点 Node($j^*$，$s^*$，BuildTree($I^-_{j^*,s^*}$，$k$)，BuildTree($I^+_{j^*,s^*}$，$k$))
如果$k$太小，会出现过拟合的情况。
同样的，一般很可能会出现同一Internal节点下出现多个预测值一样的Leaf节点。
处理方法
	正则化损失
		记$|T|$为树的Leaf节点个数，在总损失中引入这一参数
$$
		C_\alpha(T)=\sum_{i=1}^nL(T(x^{(i)}),y^{(i)})+\alpha|T|
$$
		只需要很小的一个$\alpha$值，就可以推断为不值得生成这个Leaf节点。
	Pruning
		基于新的损失来修剪树的冗余的Leaf节点。
# Ensembling
Ensembling是一种提高数据集利用率的方式。
典型的方法为Bagging，即Bootstrap Aggregating。
(Bootstrap)对于一个数据集$D_n$，我们遍历$b=1,2,3......,B$
	设$\widetilde{D}_n^{(b)}$是对$D_n$的n次随机采样（允许重复）取得的假数据集
	基于假数据集训练模型$\widetilde{f}^{(b)}$
(Aggregating)返回平均的模型$\widetilde{f}_{bag}(x)=\frac{1}{B}\sum_{b=1}^B\widetilde{f}^{(b)}(x)$
# Random Forest
随机森林是一种特殊的Bagging，针对决策树问题。
对$1,2,3,4......,B$，通过可重复采样生成$B$个假数据集。
对每一个$\widetilde{D}_n^{(b)}$
	递归直到遇到边界($k>|I|$)
		随机在$d$个维度中不重复地取$m$个维度，记为$1,2,3......,m$
		找到最佳的($m^*,s^*$)（类似于上面的找($j^*,s^*$)）
		基于此创建树节点以及其子节点。
预测时，对于回归问题，取各个树返回值的平均数。对于分类问题，返回采样点在各个树上返回值的众数（类似于各个树在投票）