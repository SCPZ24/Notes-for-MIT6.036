# K-means Algorithm
假设需要给地图（空间）上的$n$个人分配$k$个食堂。要求所有人到答自己配到的食堂距离的平方和最小。这就是一个K-means聚类（K-means Clustering）问题。
一个食堂理解为一个聚类中心（Cluster Centre）。
空间上的一个人认为一个散点。
散点$i$的坐标为$x^{(i)}$，它关联的聚类中心的索引为$y^{(i)}$
聚类中心$j$的坐标为$\mu^{(j)}$
那么，可以定义$i$点到$j$中心的Squared Loss为$|x^{(i)}-\mu^{(j)}|^2$
我们记这个系统的总平方损失为
$$
Loss=\sum_{j=1}^k\sum_{i=1}^n1\begin{Bmatrix}y^{(i)}=j\end{Bmatrix}\cdot |x^{(i)}-\mu^{(j)}|^2
$$
其中的变化因素为聚类中心的坐标$\mu$，以及每个点分配到的聚类中心$y$
我们定义K-means Objective（K-means目标）为使得这个Loss最小的$\mu,y$组合。即
$$
K\,means\,Objective=argmin_{\mu,y}\sum_{j=1}^k\sum_{i=1}^n1\begin{Bmatrix}y^{(i)}=j\end{Bmatrix}\cdot |x^{(i)}-\mu^{(j)}|^2
$$
K-means算法的实现
对于给定的聚类中心个数$k$以及最大迭代轮数$\tau$
	先执行初始化，获得最初的$\mu,y$
	然后执行$\tau$轮循环。每一轮中
		对于$n$个点，将其分配至距离最近的聚类中心。
			即对于`i in range(n)`，set $y^{(i)}=argmin_j|x^{(i)}-\mu^{(j)}|$
		然后调整每个聚类中心，将其转移至所有分配给自身的点的几何重心上
			即对于`j in range(k)`，set
	$$
				\mu^{(j)}=\frac{\sum_{i=1}^n1\begin{Bmatrix}y^{(i)}=j\end{Bmatrix}\cdot x^{(i)}}{\sum_{i=1}^n1\begin{Bmatrix}y^{(i)}=j\end{Bmatrix}}
	$$
		比对：如果上一轮迭代结束后的$y$与这一轮结束后的$y$一样，那么直接跳出循环。
	返回所得的$\mu,y$。
实际上，这个算法对于某些初始化的情况只能收敛到Local Optimal，不能收敛到Global Optimal。因此可以采取Restart：设置多个初始化的数据组，分别做K-means算法，取Loss最低的方式。
# Definition of Clustering
上述K-means算法的数据集没有Labels。K-means算法本质上实现了一种聚类（Clustering）。
聚类就是依照某些依据把数据集做拆分。
由于其不依赖Labels，因此聚类操作是Unsupervised Machine Learning的一种。
![[与无监督机器学习有关的图.png]]
# Attributes of K-means
$k$的选取
	有些情境下，$k$是给定的
	有时候$k$不给定，需要自行选取
	一般的，$k$越大，获得的Loss越小。如果$k\geq n$，那最小的Loss=0
	一般计算损失的时候，可以算一个与$k$值正相关的损失项。
$$
	Loss=\sum_{j=1}^k\sum_{i=1}^n1\begin{Bmatrix}y^{(i)}=j\end{Bmatrix}\cdot |x^{(i)}-\mu^{(j)}|^2+cost(k)
$$
K-means聚类的形态：K-means算法能完美分类等大小的圆形区域点。
![[等密度等半径聚类.png]]
![[密度不一的等量聚类.png]]
![[大样本区和散点.png]]
![[大聚团.png]]