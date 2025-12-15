# Linear Logistic Classification
有时候给出的数据集无法被Linearly Separate。
因此在交汇区域（有+1的数据点也有-1的数据点），我们可以认为是一个概率问题。
在其他区域，有产出+1的概率为1或-1的概率为1。
而在交汇区域，产出+1的概率为介于0到1中间的某值。
因此我们需要一个平滑的曲线（而非跳跃点）来描述样本-产出值的概率。
![[获得平滑概率曲线示意图.png]]
假设$A$为样本点产出的数据为+1，则$\overline{A}$表示样本数据点的产出为-1。
Linear Logistic Classification可以用于描述$P(A)$的一个函数。
典型的用于Linear Logistic Classification的函数：
$$
\begin{matrix}Sigmoid/Logistic\,\,Function\\\sigma(z)=\frac{1}{1+e^{-z}}\end{matrix}
$$
Sigmoid函数不一定能用于预测所有的情况。有时候需要对传入的数据做几何变换（乘系数θ，加常数θ）。因此可以表示为：
$$
g(x)=\sigma(\theta x+\theta_0)=\frac{1}{1+e^{-(\theta x+\theta_0)}}
$$
这里只涉及了传入的数据为一维数字的情况。实际上传入的数据点x为d维向量。
因此可以把Sigmoid函数的变量推广到d维向量的形式：
$$
\begin{matrix}Given\,d维向量x,则有d维法向量\theta\\g(x)=\sigma(\theta^Tx+\theta_0)=\frac{1}{1+e^{-(\theta^Tx+\theta_0)}}\end{matrix}
$$
![[二维数据的Sigmoid函数举例.png]]
# Linear Logistic Classification与线性分离器的统一性
Linear Logistic Classification可以看作是产出一个概率（预测为1的概率）。我们称这个式子为$Possibility=\sigma(\theta^Tx+\theta_0)$
而线性分离器的假设h产出一个确定的值，但不确保这个值对。
数学上的统一性：
	当我们令$\sigma(\theta^Tx+\theta_0)>0.5$，则依据Sigmoid函数的展开式可以化简得$\theta^Tx+\theta_0>0$。
	由此，Logistic Classification预测得概率大于0.5的条件与线性分离器预测为+1的条件相同。
然而，当数据并非线性可分时，Logistic Classification有更强的保障性。
# Negative Log Likelihood Loss
对于一个逻辑分类器($g(x)=\sigma(\theta^Tx+\theta_0)$)和一个给定的数据(已给出一个$x^{(i)}$向量和对应的$y^{(i)}$的值)，我们认为这个逻辑分类器预测对的概率为
$$
Probability(Data\,Point\,i)=\begin{cases}g(x^{(i)})\,\,\,(y^{(i)}=+1)\\1-g(x^{(i)})\,\,\,(y^{(i)}=-1)\end{cases}
$$
那么给定一个逻辑分类器和一个数据集，其预测全部正确的概率为
$$Probability(D_n)=\prod_{i=1}^nProbability(Data\,Point\,i)$$
这个概率其实反应了一个逻辑分类器的预测水平（产出可信预测的能力）。
由于这个值是很多个小于1的正数的乘积，因此会十分小。计算机的精度无法精确模拟如此小的数据。
因此可以对整个概率取对数。则上式子右边从一串乘积改为一串取完对数的结果的加和。
取对数不改变单调性，因此取完对数和也可以看作逻辑分类器预测水平的标的。
再取这个对数的相反数，则可以成为估计这个逻辑分离器预测中产生的损失的一种标的。（预测精确度越高，一方面可认为损失越小，另一方面这个相反数越小。因此这个相反数可以反应这个预测模型的损失）
我们称这组取对数再取相反数的结果为负对数似然损失（Negative Log Likelihood Loss，简称NLL损失）。
下给出公式（g为猜测，a为实际结果）。对一个数据点的情况：
$$
\begin{matrix}L_{NLL}(g,a)\\=-\log(Provavility(Data\,Point\,i))\\=\begin{cases}-\log g(x^{(i)})\,\,\,(y^{(i)}=+1)\\-\log (1-g(x^{(i)}))\,\,\,(y^{(i)}=-1)\end{cases}\end{matrix}
$$
对总体数据集的情况：
$$
\begin{matrix}总体NLL损失\\=\frac{1}{n}\sum_{i=1}^nL_{NLL}(\sigma(\theta^Tx^{(i)}+\theta_0),y^{(i)})\\=-\frac{1}{n}\sum_{i=1}^n\log(Probability(Data\,Point\,i))\end{matrix}
$$
其中$Probability(Data\,Point\,i)=\begin{cases}g(x^{(i)})\,\,\,(y^{(i)}=+1)\\1-g(x^{(i)})\,\,\,(y^{(i)}=-1)\end{cases}$
# Gradient Descent
逻辑分类器化离散为连续，可以利用基于微分的手法进行训练。
一个分类器的参数有d维向量$\theta$和标量$\theta$。一共d+1个参数。
在进行逻辑分类器的训练时，可以把所有参数统一成一组变量$\Theta$。
$$
J_{lr}(\Theta)=J_{lr}(\theta,\theta_0)=\frac{1}{n}\sum_{i=1}^nL_{NLL}(\sigma(\theta^Tx^{(i)}+\theta_0),y^{(i)})
$$
下定义梯度（Gradient）：
假设$\Theta\in R^m$，是一个m维向量。有$\Theta=\begin{bmatrix}\Theta_1,\Theta_2,\Theta_3......,\Theta_m\end{bmatrix}^T$。
对于关于$\Theta$的函数$f(\Theta)$，其梯度为
$$
Gradient\,\nabla_{\Theta}f=\begin{bmatrix}\frac{\partial f}{\partial\Theta_1},\frac{\partial f}{\partial\Theta_2},\frac{\partial f}{\partial\Theta_3}......,\frac{\partial f}{\partial\Theta_m}\end{bmatrix}^T
$$
梯度下降(Gradient Descent)是基于梯度来调整参数来使得参数组获得季小损失的算法。
梯度下降的参数：初始参数向量$\Theta_{init}$，跨度$\eta$，基于数据集确定的分类器函数$f$，梯度$\nabla_{\Theta}f$，梯度下降的临界值正数$\epsilon$，训练最大轮数$\tau$（可选可不选）。
步骤
	Initailize $\Theta^{(0)}=\Theta_{init}$
	Initailize $t = 0$
	Loop
		更新t：$t = t + 1$
		更新$\Theta$：$\Theta^{(t)}=\Theta^{(t-1)}-\eta \nabla_{\Theta}f(\Theta^{(t-1)})$
	结束循环的条件（可以依据训练需求实际情况选择其中一个或数个）：
		(1) $|f(\Theta^{(t)})-f(\Theta^{(t-1)})|<\epsilon$
		(2) $|\Theta^{(t)}-\Theta^{(t-1)}|<\epsilon$
		(3) $|\nabla_{\Theta}f(\Theta^{(t)})|<\epsilon$
		(4) $t\geq \tau$
![[二维梯度下降举例.png]]
Gradient Descent的性质：
	如果
		$f(\Theta)$是平滑的，且是下凸(convex)的
		$f(\Theta)$在$\Theta$全域上至少存在一个全局最优点
		$\eta$充分小
	那么
		经过有限轮梯度下降后，一定会找到在$\epsilon$范围内的最优点。
	注意：对于梯度下降算法来说，最优点就是最小值点。
# Regularizer
当数据集的交汇区没有值时，依据这组数据持续梯度下降下去，会使得$\Theta$的模长越来越大。同时，交汇区的曲线越来越陡峭。这就失去了逻辑回归的意义。
![[交汇区缺乏数据导致的问题举例.png]]
因此需要设置这种情况的限制因素。
使用较大的$\epsilon$算一种方法，但是容易产生其他问题。
可以引入Regularizer（正则化器）来解决这个问题。
在原来的用于梯度下降的逻辑回归函数中加入一个与$\theta$的模长有关的项。
$$
J_{lr}(\Theta)=J_{lr}(\theta,\theta_0)=\frac{1}{n}\sum_{i=1}^nL_{NLL}(\sigma(\theta^Tx^{(i)}+\theta_0),y^{(i)})+\lambda|\theta|^2
$$
其中，$R(\theta)=\lambda|\theta|^2$表示一个Regularizer（或者一个Penalty（惩罚））。
当$\theta$模长过大，其平方值在算式中就变得不可忽略，进而印象到梯度下降的方向来防止之。
Regularizer的性质：
	加入函数后，函数还是可微分且下凸的。
	$\lambda$其实是一个用于调节权重的系数。
		$\lambda$过大，Regularizer更容易对式子占主导地位
		$\lambda$过小，前面的NLLLoss更容易对式子占主导地位
定义指示函数$1(condition)$指的是condition成立时返回1；否则返回0。
把上述的$J_{lr}(\theta,\theta_0)$函数的梯度求出来则是
$$
\begin{matrix}\frac{\partial J_{lr}}{\partial \theta}=\frac{1}{n}\sum_{i=1}^n[(\sigma(\theta^Tx^{(i)}+\theta_0)-1(y^{(i)}=1))x^{(i)}]+2\lambda\theta\\\frac{\partial J_{lr}}{\partial\theta_0}=\frac{1}{n}\sum_{i=1}^n(\sigma(\theta^Tx^{(i)}+\theta_0)-1(y^{(i)}=1))\end{matrix}
$$