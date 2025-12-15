# Regress（回归）
[[Basics]]中的分类器是找到一条能大致切分平面中不同种类点的超平面的假设。返回值是+1或者-1或者+1的预测概率。
回归器是在d维空间中找到一个超平面（或曲面）来大致拟合数据点的走向。
其Label $y^{(i)}\in R$。
假设h为 $h：R^d\rightarrow R$。
![[一元回归器举例.png]]
回归器的损失采取Squared Error Loss：$L(g,a)=(g-a)^2$。
	$g,a \in R$
	其中g是回归模型的预测值，a是给定数据集对应位置的实际值。
# Linear Regression
给定一个超平面$(\theta,\theta_0)$，以及一个数据集。
对于一个位置向量$x$，这个线性回归的预测（假设）为$h(x;\theta,\theta_0)=\theta^T x+\theta_0$
则平方损失为
$$
J(\theta,\theta_0)=\frac{1}{n}\sum_{i=1}^nL(h(x^{(i)};\theta,\theta_0),y^{(i)})=\frac{1}{n}\sum_{i=1}^n(\theta^Tx^{(i)}+\theta_0-y^{(i)})^2
$$
$\theta_0$很碍眼。我们用[[Perceptron]]中的扩维操作，对所有x向量扩维，并对$\theta$向量扩维。
$$
\begin{matrix}x^{(i)}_{new}\in R^{d+1},x_{new}^{(i)}=\begin{bmatrix}x_1^{(i)},x_2^{(i)},x_3^{(i)},x_4^{(i)}......,x_d^{(i)},1\end{bmatrix}\\\theta_{new}\in R^{d+1},\theta_{new}=\begin{bmatrix}\theta_1,\theta_2,\theta_3,\theta_4......,\theta_d,\theta_0\end{bmatrix}\end{matrix}
$$
为方便后续计算，我们重新把扩维后的维数记为d维。
则平方损失为
$$
J(\theta)=\frac{1}{n}\sum_{i=1}^n(\theta^Tx^{(i)}-y^{(i)})^2=\frac{1}{n}\sum_{i=1}^n((x^{(i)})^T\theta-y^{(i)})^2
$$
为方便表示，我们直接定义数据集中的位置向量集为$n×d$矩阵（同一向量以行排列）
$$
\widetilde{X}=\begin{bmatrix}x_1^{(1)}\,\,x_2^{(1)}\,\,......\,\,x_d^{(1)}\\x_1^{(2)}\,\,x_2^{(2)}\,\,......\,\,x_d^{(2)}\\......\\x_1^{(n)}\,\,x_2^{(n)}\,\,......\,\,x_d^{(n)}\end{bmatrix}
$$
再定义数据集中的y值集为$n×1$矩阵
$$
\widetilde{Y}=\begin{bmatrix}y^{(1)}\\y^{(2)}\\...\\y^{(n)}\end{bmatrix}
$$
由于$(x^{(i)})^T\theta-y^{(i)}$产出一个数字，则$\widetilde{X}\theta-\widetilde{Y}$产出一个$n×1$列向量。
则有
$$
J(\theta)=\frac{1}{n}\sum_{i=1}^n((x^{(i)})^T\theta-y^{(i)})^2=\frac{1}{n}|\widetilde{X}\theta-\widetilde{Y}|^2=\frac{1}{n}(\widetilde{X}\theta-\widetilde{Y})^T(\widetilde{X}\theta-\widetilde{Y})
$$
由于$J(\theta)$的表达式是一个关于$\theta$的二次多项式，因此可以通过公式直接求出最低点。
当梯度为$\overrightarrow{0}$，可以认为这个点是这个函数的最小值点。有
$$
\nabla_{\theta}J(\theta)=\frac{2}{n}\widetilde{X}^T(\widetilde{X}\theta-\widetilde{Y})=\overrightarrow{0}
$$
展开、移项再化简得
$$
\theta=(\widetilde{X}^T\widetilde{X})^{-1}\widetilde{X}^T\widetilde{Y}
$$
取这个$\theta$，就获得了最优的线性回归器。
# Ridge Regression
有时候，这个$\theta$并非唯一。
	直观上的成因：数据坍缩成维度更低的形式（比如原本分布于二维平面上的点集现在只分布于或近似只分布于一条直线上。那拟合结果作为一个平面，自然有过这条线的无数种可能）。
	![[拟合结果非唯一的数据集举例.png]]
	梯度层面的反应：梯度为0的点不止一个点而是有无数个点（比如下图右图中的情况，梯度为0的点其实分布于一条线上）。
	![[拟合结果非唯一的梯度视角.png]]
	代数本质：数据集$\widetilde{X}$的秩小于d。
		此时$R(\widetilde{X}^T\widetilde{X})<d$，d元线性方程组 $\widetilde{X}^T\widetilde{X}\theta=\widetilde{X}^T\widetilde{Y}$的解非唯一，为一个解集。（上述方程组就是$\theta=(\widetilde{X}^T\widetilde{X})^{-1}\widetilde{X}^T\widetilde{Y}$的前身)
		$|\widetilde{X}^T\widetilde{X}|$为0或几乎为0，则$\widetilde{X}^T\widetilde{X}$不存在逆矩阵。无法直接求出$\theta$。因此看到这个行列式为0或近似0，那直接认为理论上可求出的$\theta$不唯一。
解决方法：岭回归(Ridge Regression)。
核心思想是虽然理论上只能确定无限个$\theta$，我们添加一个条件：要使$|\theta|$尽可能小。
这时$\theta$就会受这个制约条件限制而收敛向一个尽可能使得$|\theta|$小的值。
类似正则化，岭回归也可以配一个与$|\theta|$有关的量。
扩维前的表达式为
$$
J_{ridge}(\theta,\theta_0)=\frac{1}{n}\sum_{i=1}^n((x^{(i)})^T\theta+\theta_0-y^{(i)})^2+\lambda|\theta|^2
$$
下重点看扩维后的情形。扩维后的表达式为
$$
J_{ridge}(\theta)=\frac{1}{n}|\widetilde{X}\theta-\widetilde{Y}|^2+\lambda|\theta|^2=\frac{1}{n}(\widetilde{X}\theta-\widetilde{Y})^T(\widetilde{X}\theta-\widetilde{Y})+\lambda|\theta|^2
$$
其中的$\lambda|\theta|^2$类似于[[Logistic Regression]]中Regularizer方法中的penalty。
$\lambda$是一个极小的正量，用于配权。
令$\nabla_{\theta}J_{ridge}(\theta)=0$，可以得出
$$
\theta=(\widetilde{X}^T\widetilde{X}+n\lambda E_d)^{-1}\widetilde{X}^T\widetilde{Y}
$$
其中$E_d$是d阶单位矩阵。
其中，$\widetilde{X}^T\widetilde{X}+n\lambda E_d$是一个可逆（Invertible）矩阵。
Tips
	用于加入训练的数据集中的一列数据，其数量级和分布对之后的$\theta$可能产生较大影响。因此可以进行[[DataSets Preprocessing]]中的数据标准化操作。
	上述回归模型依然可以用[[DataSets Preprocessing]]中的Featurization来处理非数字类型的数据。
# Gradient Descent for Regression
其实使用公式来求最优$\theta$看似很快（只有一步迭代），但是实际上这个过程中涉及到求逆矩阵。
求逆矩阵的时间复杂度为$O(n^3)$（其中n为矩阵阶数）。这导致这样操作很耗时。
实际上也可以用梯度下降来实现训练。
这样虽然损失了精确性，但是减少了训练所需工作量。
下直接给出$J(\theta,\theta_0)$（扩维前）关于$\theta$，$\theta_0$的偏导数，由此可以直接求出梯度：
$$
\begin{matrix}\nabla_\theta J_{ridge}=\frac{2}{n}\sum_{i=1}^n[((x^{(i)})^T\theta+\theta_0-y^{(i)})x^{(i)}]+2\lambda\theta\\\frac{\partial J_{ridge}}{\partial\theta_0}=\frac{2}{n}\sum_{i=1}^n((x^{(i)})^T\theta+\theta_0-y^{(i)})\end{matrix}
$$
其中，$\theta$是由多个实数组成的向量。给出$J_{ridge}(\theta,\theta_0)$关于$\theta$的梯度也可以当偏导数用。其梯度为$\begin{bmatrix}\nabla_\theta J_{ridge}\\\frac{\partial J_{ridge}}{\partial\theta_0}\end{bmatrix}$。
# Othor Loss Example for Regression
$$ \text{RMSE} = \sqrt{ \frac{1}{n} \sum_{i=1}^n \left( y^{(i)} - f(x^{(i)}) \right)^2 } $$