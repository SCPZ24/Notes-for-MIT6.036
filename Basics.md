# Data Set and Hypothesis
在机器学习中，数据可以表示为vector的形式。
一个d维欧几里得空间中的一个vector x为
$$
x = (x_1,x_2,x_3,......,x_d)
$$
设一个数据集有n个向量。则表示为(右上角括号里的数不是指数，而可以理解为上标，表示数据集中第i个向量)
$$
\begin{matrix}可记数据集(Training data)为D_n\\则i \in \begin{Bmatrix}{1,2,3,......,n}\end{Bmatrix}\\x^{(i)} = (x_1^{(i)},x_2^{(i)},x_3^{(i)},......,x_d^{(i)})\end{matrix}
$$
标记器Label：y(x)为输出端。一个vector x可以对应一个输出y。
当y为一个二元输出结果时，可以定义一个假设h
$$
\begin{matrix}Label\,\,\,\,y \in \begin{Bmatrix}-1,+1\end{Bmatrix}\\Define \,Hypothesis\\h:R^d\rightarrow\begin{Bmatrix}-1,+1\end{Bmatrix}\\其中R^d为定义在d维上的欧几里得空间\end{matrix}
$$
依据一个假设h，可以定义一个假设函数：y = h(x)
假设集H：所有假设h形成的集合记为H。
# Linear Classifier
![[线性分离器的推导示意图.png]]
如图，任意一个给定的vector θ，由其方向可以确定无数条垂直于θ的直线（红线）。
对于所有起点位于远点，终点落在某一条红线上的vector x，有
$$
\frac{\theta^T\cdot x}{|\theta|} = a 
$$
把常数统一，该式子可以化成
$$
\theta^T\cdot x + \theta_0 = 0
$$
不难得出
$$
\begin{matrix}以\theta^T\cdot x + \theta_0=0为分界线\\\theta^T\cdot x + \theta_0 \geq  0表示\theta正方向上的空间\\\theta^T\cdot x + \theta_0 \leq  0表示\theta负方向上的空间\end{matrix}
$$
则依据线性分类器，可以定义假设
$$
h(x,\theta,\theta_0) = \begin{cases}+1(\theta^T\cdot x + \theta_0 \geq  0)\\-1(\theta^T\cdot x + \theta_0 < 0)\end{cases}
$$
其中，θ和θ0为参数(parameters)，表述的是假设本身的性质。而x是变量，是假设中的因子用于确定y。
假设集H是所有如此定义的h的集合。
# 判断假设的好坏：Loss Assessment
假设应该能够用于在新的情况下预测出正确的结论。
因此可以用这个能力确定判定的好坏。
可以用损失函数L(Loss)来记录当预测错误或偏差时，造成的损失。
记依据假设给出的预测值是g(Guess) ，而实际值是a(Actual)。则可以定义L(g,a)。
比如
0-1 loss
$$
L(g,a) = \begin{cases}0(a=g)\\1(a\neq g)\end{cases}
$$
asymmetric loss（非对称损失，强调一些预测失误的情况损失极大，需要优先避免）
$$
L(g,a)=\begin{cases}1(g=1,a=-1)\\100(g=-1,a=1)\\0(else)\end{cases}
$$
用L(g,a)检测平均误差
$$
\begin{matrix}基于n'个新的样例获得Test\,\,\,Error\\\varepsilon(h,D_{new\,n^{'}})=\frac{\sum_{i=n+1}^{n+n'}L(h(x^{(i)}),y^{(i)})}{n'}\\基于原有n个样例获得Test\,\,\,Error\\\varepsilon_n(h,D_n)=\frac{\sum_{i=1}^{n}L(h(x^{(i)}),y^{(i)})}{n}\end{matrix}
$$
获得的平均误差更小的h认为更优。
# Concept of Learning Algorithm
![[学习算法功能示意图.png]]
一个假设可以根据数据集中的一组数据获得一个预测。
学习算法可以基于数据集Dn获得一个较优的假设来用于更好的预测。
一个简易的学习功能实现
	执行k次循环：
		随机取样θ，θ0，形成一个假设h。
		计算这个h的平均误差。
		再随机取样。直到k次循环全部结束。
	记录并返回所有h中，使得平均误差最小的h。