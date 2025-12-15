# State Machine
状态机的组成：
$S$：所有可能状态$s$的集合
	$s_0$：起始状态
	所有状态满足马尔科夫性，即下一状态和奖励仅与当前状态和动作有关，与历史无关。
$A$：所有可能输入$a$（操作）的集合
对于一个操作，在某个状态下给出，它有可能在各个概率下转化为各个其他状态
则有转化矩阵
$$
Matrix_a=\begin{bmatrix}p_{s_1\rightarrow s_1}\,\,p_{s_1\rightarrow s_2}\,\,p_{s_1\rightarrow s_3}......p_{s_1\rightarrow s_n}\\p_{s_2\rightarrow s_1}\,\,p_{s_2\rightarrow s_2}\,\,p_{s_2\rightarrow s_3}......p_{s_2\rightarrow s_n}\\......\\p_{s_n\rightarrow s_1}\,\,p_{s_n\rightarrow s_2}\,\,p_{s_n\rightarrow s_3}......p_{s_n\rightarrow s_n}\end{bmatrix}
$$
$f:S × A \rightarrow S$：函数，输入一个起始状态以及一个输入操作，映射从一种状态转化为另一种状态。
$T$：Transition Model。给定原状态和操作和后续状态，返回转变为该后续状态的概率。
	$P(s_t|s_{t-1},a_{t-1})=T(s_{t-1},a_{t-1},s_t)$。
$R$：奖励函数，指某状态下执行操作会有多少受益。$S × A \rightarrow R$。
	$R(s,a)$为该轮收益
# Policy
策略$\pi$。输入一个状态，输出一个操作。$\pi : S \rightarrow A$。
期限(Horizon)$h$：总共可以进行操作的轮数（一轮操作获得一次收益）
总受益$V$。输入一个状态，给出对应策略。
$V_\pi^h(s)$表示在剩余期限为h轮，策略集为$\pi$，初始状态为$s$的状况下的总收益。
则有递推公式
$$
V_\pi^h(s)=R(s,\pi(s))+\sum_{s^{'}\in\, S}T(s,\pi(s),s^{'})\cdot V_\pi^{h-1}(s^{'})
$$
上述的$\pi$为non_stationary的。因为其只和s有关。
实际上，策略还应该与剩余轮数$h$有关，记为$\pi_h(s)$。
# Seeking Best Policy
## Finite Horizon
$Q^h(s,a)$：在当前状态为s，还剩h轮时。我们这一轮采取操作a，那么假设接下来h-1轮我们都能采取了最佳操作，我们说这样操作的总收益为$Q^h(s,a)$。
有了q的概念，我们可以找到一个optimal policy：$\pi_h^*(s)=argmax_aQ^h(s,a)$。即所有a中，使得$Q^h(s,a)$最大的那个a。
则有最大收益的递推公式
$$
Q^h(s,a)=R(s,a)+\sum_{s^{'}}T(s,a,s^{'})max_{a^{'}\in A}Q^{h-1}(s^{'},a^{'})
$$
## Infinite Horizon
当$h\rightarrow +\infty$，我们认为可以操作并收益无限轮。
这时，时间成本应该被计入：越晚获取的收益，相对于第一轮获取的收益就越不值钱。(Horizon非无限的时候其实也可以引入$\gamma$，只不过其影响一般不大)
我们引入一个Discount Factor $\gamma \in (0,1)$ 。表示物品价值的折损率。
从第一轮开始，经过$t$轮后，其价值相对于第一轮收益的折损表示为$\gamma^t$。
以钱为标的，用$y^{-1}$表示每轮货币通货膨胀的比率。比如一带米，第1年为1元，第2年就为$\gamma^{-1}$元。第t+1年为$\gamma^{-t}$元。
假设我每一轮弄到1袋米时间，则总收益为
$$
V=1+\gamma+\gamma^2+\gamma^3+......=\frac{1}{1-\gamma}
$$
从单调性来看，$\gamma$越小，价值缩水的越快，总收益越小，则$V$越小。
我们记初始状态为$s$，策略集为$\pi:s\rightarrow a$，则无穷期限的总收益$V_\pi(s)$为
$$
V_\pi(s)=R(s,\pi(s))+\gamma\sum_{s^{'}\in S}T(s,\pi(s),s^{'})V_\pi(s^{'})
$$
往方程里分别代入$S$集合中的所有$s$，这个方程可以写出由$|S|$个线性方程组成的线性方程组。
记$n=|S|,S=\begin{Bmatrix}s_1,s_2,s_3......,s_n\end{Bmatrix}$，
则每一个可以整理为
$$
V_\pi(s_i)-\gamma\sum_{i=1}^nT(s_i,\pi(s_i),s_j)V(s_j)=R(s_i,\pi(s_i))
$$
矩阵表示为
$$
(E-\gamma P)V = R
$$
其中
	$E$为$n$阶单位矩阵。
	$P$为转移概率矩阵，$P_{ij}=T(s_i,\pi(s_i),s_j)$。
	$V$为价值函数向量，为待求的未知数。
	$R$为即时奖励向量。
$\gamma$小于1时，可保证矩阵可逆，则可解出唯一的解向量$V$。
对于最优策略：假设$s$状态$a$操作之后，做出的每一步策略都是最优策略得到的总收益为$Q(s,a)$，则有
$$
Q(s,a)=R(s,a)+\gamma\sum_{s^{'}\in S}T(s,a,s^{'}){max}_{a^{'}\in A}Q(s^{'},a^{'})
$$
则认为最优策略为
$$
\pi_{Q^*}(s)=argmax_aQ^*(s,a)
$$
求取最优策略的方法之一：Policy Iteration
记第k轮策略集为$\pi_k$，价值函数$V_{\pi_k}$，则有线性方程组
$$
(E-\gamma P_{\pi_k})V_{\pi_k} = R_{\pi_k}
$$
接下来有了确知的$V_{\pi_k}$，基于此改进策略
	对每个状态$s$，选择使得接下来的总收益值最大的那个$a$作为$\pi_{k+1}(s)$。即
$$
	\pi_{k+1}(s)=argmax_a[R(s,a)+\gamma\sum_{s^{'}}T(s,a,s^{'})V_{\pi_k}(s^{'})]
$$
直到我们发现某一轮后有$\pi_{k+1}=\pi_k$，说明收敛结束，得到最佳策略$\pi^*$。