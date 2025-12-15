# Convolution
## Filter
采用filter，对图像或一维序列取每个局部。在对应位置乘权重最后加和，然后加上偏移量形成新的图像或一维序列的操作。
![[一维卷积举例1.png]]
如上图，把最上面的序列依次乘filter上的权重再相加形成新值，再把新值排列形成新序列。
![[一维卷积举例2.png]]
这个过程称为Convolution（卷积）。
卷积后序列大小减少，比如上图中的10长度序列卷积完产出8长度序列。
可以采取对原数据的填充（Padding）。即在信息的边缘同时补一个值（默认补0），再卷积，即可确保产出的信息不损失大小。
![[一维卷积的Padding举例.png]]
偏移量（Bias）：对卷积完后的值再加一个数字。
比如上述图没有再加数字，那结果如上图。
如果加了偏移量，则结果序列为1,0,1,0,1,-1,2,0,1,1。
二维图像（假设颜色只有0和1）也是同理，此时filter也是二维的。
![[二维卷积举例.png]]
Filter的维度和大小（shape）是可以变的。
	一维中，不止可以用长度3的Filter。可以用别的长度，甚至可以跳着采样。
	其他维度也是同理。
## Dimensions
一维的数据可称为向量（Vector）
二维的数据可称为矩阵（Matrix）
三维的数据可称为张量（Tensor）
## Parameters
Filter中与原图像相乘的数为权重（Weight）。
	$a×b$的Filter，其参数（权重）为$w_1,w_2,w_3......,w_{ab-1},w_{ab}$
Filter采集完后再加的数字为偏移量（Bias）
# Activation
卷积完可以用激活函数进一步处理。
一般采用[[Neural Network]]中提到的ReLU函数。
![[卷积后激活举例.png]]这一次卷积+激活，实际上是找到了原一维序列中孤立的1。
对于同一张图片，不止可以采用一次Convolution+Activation的操作。
称一次Convolution+Activation操作为一个Channel（通道）。
实际上可以采取多次。
假设采取了n次不同的Convolution+Activation操作，则称这一层的通道数为n。
![[多通道示意图.png]]
# Max Pool
Max Pooling（最大池操作）：一种特殊的Filter操作，每次返回Filter覆盖区域中最大的数值。
参数
	size（shape），即这个Filter一次覆盖的区域。
	stride（步长）：一次Filter结束后，跨步的距离。
比如Filter的size为3，步长为1，则最大池操作为
![[大小3步长1Filter举例.png]]
当Filter的size为3，步长为3，则产出的结果矩阵会更小
![[步长3最大池操作举例.png]]
# Typical Architecture of CNN
![[卷积神经网络一般架构示意图.png]]
获得Input，经过多次卷积+线性整流产生最终图像。（Feature Learning）
然后扁平化后再做处理和提取获得结果。（Classification）
	扁平化后的数据其实可以看做一个一维向量。
	因此可以做前面已经有的[[Logistic Regression]]、[[Regression Model]]（线性回归），或再用[[Neural Network]]操作。
# Backpropagation
反向传播可以用来求神经网络中某一层中参数的梯度。
下面以一个仅有2层的卷积神经网络为例。
输入为一个$5×1$列向量$X$。
Filter为一个$3×1$列向量$W^{(1)}$。
Pad入$X_0,X_6$，则Filter后得结果为$5×1$列向量$Z^{(1)}$。
第一层的激活函数为ReLU，结果为$5×1$列向量$A^{(1)}$。
第二层直接左乘一个$5×1$列向量的转置$(W^{(2)})^T$。为$A^{(2)}=(W^{(2)})^TA^{(1)}$。结果是一个数。
损失函数
$$
L(A^{(2)},y)=(A^{(2)}-y)^2
$$
$W^{(1)}$为隐藏层的参数。要求其梯度需要用链式法则。有
$$
\frac{\partial L}{\partial W^{(1)}}=\frac{\partial Z^{(1)}}{\partial W^{(1)}}\cdot\frac{\partial A^{(1)}}{\partial Z^{(1)}}\cdot\frac{\partial L}{\partial A^{(1)}}
$$
记$a×b$矩阵为$M[a,b]$，维度为k的列向量为$V[k]$。则有向量相偏导数的结果为
$$
\frac{\partial V[a]}{\partial V[b]}=M[b,a]
$$
则可验证上述链式法则的维数合理性
$$
\begin{matrix}\frac{\partial V[1]}{\partial V[3]}=\frac{\partial V[5]}{\partial V[3]}\cdot\frac{\partial V[5]}{\partial V[5]}\cdot\frac{\partial V[1]}{\partial V[5]}\\M[3,1]=M[3,5]\cdot M[5,5]\cdot M[5,1]\end{matrix}
$$
完全合理。下关注其中一个。以$\frac{\partial Z^{(1)}}{\partial W^{(1)}}$为例
我们记$Z^{(1)}$的分量为$Z_1^{(1)},Z_2^{(1)},Z_3^{(1)},Z_4^{(1)},Z_5^{(1)}$，$W^{(1)}$的分量为$Z^{(1)}$的分量为$W_1^{(1)},W_2^{(1)},W_3^{(1)}$。
则有
$$
\frac{\partial Z^{(1)}}{\partial W^{(1)}}=\begin{bmatrix}\frac{\partial Z_1^{(1)}}{\partial W_1^{(1)}}\,\,\frac{\partial Z_2^{(1)}}{\partial W_1^{(1)}}\,\,\frac{\partial Z_3^{(1)}}{\partial W_1^{(1)}}\,\,\frac{\partial Z_4^{(1)}}{\partial W_1^{(1)}}\,\,\frac{\partial Z_5^{(1)}}{\partial W_1^{(1)}}\\\frac{\partial Z_1^{(1)}}{\partial W_2^{(1)}}\,\,\frac{\partial Z_2^{(1)}}{\partial W_2^{(1)}}\,\,\frac{\partial Z_3^{(1)}}{\partial W_2^{(1)}}\,\,\frac{\partial Z_4^{(1)}}{\partial W_2^{(1)}}\,\,\frac{\partial Z_5^{(1)}}{\partial W_2^{(1)}}\\\frac{\partial Z_1^{(1)}}{\partial W_3^{(1)}}\,\,\frac{\partial Z_2^{(1)}}{\partial W_3^{(1)}}\,\,\frac{\partial Z_3^{(1)}}{\partial W_3^{(1)}}\,\,\frac{\partial Z_4^{(1)}}{\partial W_3^{(1)}}\,\,\frac{\partial Z_5^{(1)}}{\partial W_3^{(1)}}\end{bmatrix}
$$
带入有
$$
\frac{\partial Z^{(1)}}{\partial W^{(1)}}=\begin{bmatrix}X_0\,\,X_1\,\,X_2\,\,X_3\,\,X_4\\X_1\,\,X_2\,\,X_3\,\,X_4\,\,X_5\\X_2\,\,X_3\,\,X_4\,\,X_5\,\,X_6\end{bmatrix}
$$
同理求出其他矩阵，再相乘得出梯度。