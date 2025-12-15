# Activation Function
激活函数一般是非线性的函数，使得神经网络能够学习复杂模式。
最原始的模型为Step Function，但是由于其导数处处为0，因此不适合用于模型训练。
$$
StepFunction:\Phi(x)=1\begin{Bmatrix}w^Tx+w_0>=0\end{Bmatrix}
$$
## 常用激活函数
Sigmoid函数
$$
\sigma(x)=\frac{1}{1+e^{-x}}
$$
优点：可把原先的0-1二元输出改为输出概率（适合二分类输出）
缺点：$|x|$较大时，梯度小，梯度下降慢。
tanh函数
$$
tanh(x)=\frac{e^x-e^{-x}}{e^x+e^{-x}}
$$
把+1，-1的标的改为(-1,+1)区间内连续值的输出。
ReLU函数
$$
ReLU(x)=\begin{cases}x\,\,\,(x>0)\\0\,\,\,(x<=0)\end{cases}
$$
Leaky ReLU
$$
LeakyReLU(x)=\begin{cases}x\,\,\,(x>0)\\\alpha x\,\,\,(x<=0)\end{cases}
$$
其中$\alpha$通常取0.01
激活函数通过对数据集的处理并叠加产生新的数据集。
![[激活函数举例图.png]]
# Layer of Neural Network
对于一个数据集，取其中一个向量x来讨论
作为第一层Input，其为一个$m^{(1)}×1$向量。
其输出为$A^{(1)}$，为一个$n^{(1)}×1$的向量，满足$A_i^{(1)}=f^{(1)}(w_i^{(1)T}x+w_i^{1})，其中i \in \begin{Bmatrix}1,2,3......,n^{(1)}\end{Bmatrix}$。
把所有的$A_i^{(1)}$纵向拼成一个大的列向量作为第一个Layer的输出。
接下来重新定义$f^{(i)}$：它可以是一个激活函数。我们认为其不止作用于一个数，而是作用于一个列向量。即对列向量的每一个数都做同样的动作，然后把对应的结果生成一个新的列向量。
则有
$$
A^{(1)}=f^{(1)}(W^{(1)T}x+W_0^{(1)})
$$
其中，$W^{(1)}$为$m^{(1)}×n^{(1)}$矩阵，$W_0^{(1)}$为$n^{(1)}×1$向量。
对于下一层（第二层），有$m^{(2)}=n^{(1)}$。即上一层的输出向量为下一层的输入向量。
接下来进行类似的处理。
$$
A^{(2)}=f^{(2)}(W^{(2)T}A^{(1)}+W_0^{(2)})
$$
直到最后一层。
整体来看
$$
A(last) = NN(x,W,W_0)
$$
# Function Graph
以图表示神经网络
每一层(Layer)的结构：Inputs-Dot Product(线性变换)-Pre-activation(图中Z列)-Activation Function-Activation(图中A列)
![[神经网络的一层示意图.png]]
中间的操作步骤视为一个神经元(neuron/unit/node)。则图中这一层有$n^{(1)}$个神经元。
Fully Connected
	对于层：一个层中的每一个输入的向量进行的操作都相同，产出对应量的输出向量。
	对于神经网络：一个神经网络中的所有层都是Full Connected，则这个神经网络也是Fully Connected。
对于一个神经网络中的层
	最后一层为输出结果的层，称为输出层(Output Layer)。
	对于输出层前面的层，称为隐藏层(Hidden Layer)。
每一层都可以部署回归或分离器的神经元。