# Perceptron Algorithm（感知器算法）
![[感知器算法流程图.png]]
初始化后，预设进行τ次调整（有些数据无法在有限次调整后完成学习）。
if语句后面的含义
$$
\begin{matrix}预测反应结果正确的情况\begin{cases}y^{(i)}=+1且\theta^Tx^{(i)}+\theta_0>0\\y^{(i)}=-1且\theta^Tx^{(i)}+\theta_0<0\end{cases}\\反应结果错误的情况（需要进入if之后的调整语句）\begin{cases}y^{(i)}与\theta^Tx^{(i)}+\theta_0异号(预测错误)\\x^{(i)}=\overrightarrow{0}且\theta_0=0(刚初始化完)\\\theta^Tx^{(i)}+\theta_0=0(样本点落在分界超平面上)\end{cases}\\当向量空间维度为d，超平面指的就是d-1维的面。\\一个超平面可以线性地把d维空间分成两片。\end{matrix}
$$
更新操作的效果
![[更新操作的效果示意图.png]]
更新后，把跟新的数据代入if后面的表达式左侧，可以发现化简完比原来多出一个恒正的量。因此更新后的假设更有可能做正确的预测。
但是依据原数据进行这样一次更新，必不一定能让更新后的假设预测原数据取得正确的结果。
如果每次更新都计算一次对于所有样本的Test Error，则一次更新后的Test Error不一定会比上次小。因此训练中还是需要记录使得Test Error最小的h，并确保感知器算法的输出结果要么是这个h，要么是循环跳出后最终的h。
# Linearly Separable（线性可分性）
线性可分性是对于数据集的性质。其表述为正负的点一定可以被一个超平面完美切分（一侧的样本全为正，一侧的样本全为负，即所有样本数据可以被线性分类器正确分类）。
数学语言表述：
$$
\begin{matrix}If\,\,there\,\,exists\,\,\theta\,\,and\,\,\theta_0,\,\,such\,\,that\\for\,\,every\,\,point\,\,index\,\,i\in\begin{Bmatrix}1,2,3,4,5......,n\end{Bmatrix}\\we\,\,have\,\,y^{(i)}(\theta^Tx^{(i)}+\theta_0)>0\\Then\,\,we\,\,verdict\,\,DataSet\,\,D_n\,\,as\\Linearly\,\,Separable.\end{matrix}
$$
# Margin of DataSet
可以推导出空间中一点x* 与一个超平面(θ，θ0)的有向距离为（在θ指向的方向为正，在θ指向的方向的反方向为负）：
$$
distance(x^*,\theta,\theta_0)=\frac{\theta^Tx^*+\theta_0}{|\theta|}
$$
基于有向距离的定义，下给出Margin of the Labelled Point的定义（默认为对于超平面θ，θ0）：
$$
Margin(x^{(i)})=y^{(i)}(\frac{\theta^Tx^*+\theta_0}{|\theta|})
$$
可以认为点对超平面的Margin也是有向的。当这个点被预测正确时，这个值为正；预测错误时，这个值为负或者0。
基于点对超平面的Margin，下定义一个DataSet对于一个超平面的Margin（默认为对于超平面θ，θ0）：
$$
Margin(D_n)=min_{i=\begin{Bmatrix}1,2,3,4......,n\end{Bmatrix}}Margin(x^{(i)})
$$
因此可以知道，如果一个线性分类器未能把一组数据完美分类，则这个数据集对其超平面的Margin(Dn)一定不大于0。
# Theorem of Perceptron Performance
对于满足如下条件的DataSet：
$$
Assumptions\begin{cases}Hypothesis对应的超平面经过空间的原点（超平面的\theta_0=0）\\\\存在\gamma(\gamma>0)与\theta^*，使得对有所数据点i\in\begin{Bmatrix}1,2,3,4......,n\end{Bmatrix}，满足Margin(x^{(i)})>\gamma\\即y^{(i)}(\frac{\theta^Tx^*}{|\theta|})>\gamma\\\\存在R(R>0)，使得对所有的数据点i\in\begin{Bmatrix}1,2,3,4......,n\end{Bmatrix}，满足|x^{(i)}|\leq R\end{cases}
$$
可以得出如下结论：
$$
上述的Perceptron\,\,Algorithm可以在(\frac{R}{\gamma})^2次更新内，完成学习，产出完美的线性分离器。
$$
实际上，不是所有数据集都能找到过原点的分类器。
我们可以将数据集和分类器升维来满足过原点的需求：
$$
\begin{matrix}Initial:\\x\in R^d,\theta\in R^d,\theta_0\in R\\Point\,x:\theta^Tx+\theta_0=0\\Update \,\,Dimension:\\x_{new}\in R^{d+1},x_{new}=\begin{bmatrix}x_1,x_2,x_3,x_4......,x_d,1\end{bmatrix}\\\theta_{new}\in R^{d+1},\theta_{new}=\begin{bmatrix}\theta_1,\theta_2,\theta_3,\theta_4......,\theta_d,\theta_0\end{bmatrix}\\Then\,\,we\,\,have:\\\theta_{new}^Tx_{new}=0\\注意到\theta_{new}^Tx_{new}与\theta^Tx+\theta_0值一样，则正负性一样，\\则输入同一数据点，升维后的分类器（假设）依然能给出与之前一致的返回值。\end{matrix}
$$
因此上述结论可以推广到θ0≠0的情况。