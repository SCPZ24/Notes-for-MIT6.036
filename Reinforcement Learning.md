# Definition
与[[Markov Decision Process]]不同的是，强化学习是当智能体进入一个陌生的环境中，并不知道奖励和转换矩阵，智能体需要做出操作并依据反馈学习周围的环境。
即进入陌生环境后，依然有状态机$S$和操作集合$A$，但不知道所有的转移概率$T$与奖励$R$。
# Exploration & Exploitation
智能体笼统地有两种策略：探索和利用。
智能体被投放入陌生环境后，假设会进行无限轮操作。其目的是获取尽可能大的Reward。
Exploration策略为探索环境中的信息
	操作为不管环境为何种情况，完全随机选择一个$a\in A$当做该轮操作。
Exploitation为基于获取的信息做出最优的决策
	操作为基于搜集到的信息和当前的$s$决策出最优的行为$a$。
为了获得更好的Reward，智能体需要权衡Exploration和Exploitation的操作比例。
我们用$\epsilon$来表示权衡的比例。
$\epsilon\in (0,1)$，我们认为有$1-\epsilon$的概率采取Exploitation策略，有$\epsilon$的概率采取Exploration策略。
实际上，每一步操作都会有信息的摄入，即$R(s,a)，s_{new}$。
# Searching for Optimal Policy By $T$ and $R$
可以通过持续从环境中学习到更准确的$T$和$R$值。
	初始化智能体状态：$s^{(1)}=s_0$
	初始化$T$：对任何的$s,a,s^{'}$，我们有$\widehat{T}(s,a,s^{'})=\frac{1}{|S|}，\widehat{R}(s,a)=0$
	对于第$t$轮迭代：
		基于$\epsilon$选择操作$a^{(t)}$。
		执行操作$a^{(t)}$，获得更新的该情况下的收益$r^{(t)}$与下一轮得到的状态$s^{(t+1)}$。
		更新：
			$\widehat{R}(s^{(t)},a^{(t)})=r^{(t)}$
			$\widehat{T}(s,a,s^{'})=\frac{1+\sum_{i=1}^t1(s^{(i)}=s,a^{(i)}=a,s^{(i+1)}=s^{'})}{|S|+\sum_{i=1}^t1(s^{(i)}=s,a^{(i)}=a)}$
				实质即假设在$s$状态下的$a$操作中，原本变为任何一个$s^{'}$的情况都发生过1次。
				随着迭代，如果某轮发现$s$状态下的$a$操作后产出一个$s^{'}$，那变为$s^{'}$的情况计数（频数）加一。
				若干次迭代后，可以依据频数推出各个$s^{'}$的$\widehat{T}(s,a,s^{'})$。
				数据量充足后，各个$s^{'}$初始化默认发生过的1次会收敛掉。
			依据新的$\widehat{R},\widehat{T}(s,a,s^{'})$预测新的$Q$以及更新策略$\pi$。
在实际操作中，$\epsilon$不一定为常数。起初，可以让$\epsilon$大一些，随着探索轮数变多，其实可以认为对环境系统的认知已经收敛至真实情况，这时可以让$\epsilon$变小。
# Searching for Optimal Policy By $Q$
## Expected Values
首先讨论一下各种期望值。
经典期望值
$$
\widetilde{E}^{(t)}=\frac{1}{t}\sum_{i=1}^tx^{(i)}
$$
运行时期望值：每一轮产生一个期望值，新输入值之后基于迭代轮数、旧期望值产生新期望值。
已知$\widetilde{E}^{(0)}=0，\alpha^{(t)}=\frac{1}{t}$，则有
$$
\widetilde{E}^{(t)}=(1-\alpha^{(t)})\widetilde{E}^{(t-1)}+\alpha^{(t)}x^{(t)}
$$
变化版运行时均值：任何$\alpha^{(t)}$都为一个常数$\alpha$。
$$
\widetilde{E}^{(t)}=(1-\alpha)\widetilde{E}^{(t-1)}+\alpha x^{(t)}
$$
可由递推得通项公式：$\widetilde{E}^{(t)}=\sum_{i=1}^t(1-\alpha)^{t-i}\alpha x^{(t)}$
运行时均值其实对后输入的值权重更大。
## Estimate Q
已有Q的迭代公式
$$
Q_{new}=R(s,a)+\gamma\sum_{s^{'}\in S}T(s,a,s^{'})max_{a^{'}}Q_{old}(s^{'},a^{'})
$$
化成概率×值加和的形式为
$$
Q_{new}=\sum_{s^{'}\in S}T(s,a,s^{'})(R(s,a)+\gamma max_{a^{'}}Q_{old}(s^{'},a^{'}))
$$
这就是一个均值的形成方式。
基于上述的变化版运行时均值，可以把这个公式近似成用于迭代更新$Q(s,a)$的方法(其中箭头表示取代被指向的值)
$$
Q(s,a)\leftarrow (1-\alpha)Q(s,a)+\alpha(R(s,a)+\gamma max_{a^{'}}Q_{old}(s^{'},a^{'}))
$$
公式中保留$Q_{old}$作用不大，直接用当前轮的$Q$替换$Q_{old}$；$R(s,a)$其实就是这一轮读取到的Reward，记为$r$。则有简化版迭代公式
$$
Q(s,a)\leftarrow (1-\alpha)Q(s,a)+\alpha(r+\gamma max_{a^{'}}Q(s^{'},a^{'}))
$$
可以用这种方法替换掉上一种学习方式中对$T,R$的迭代。
当需要采取Exploitation策略时：对于给定$s$的每一步决策，我们对于任何$a$，直接搜索所有的$Q(s,a)$。取使得$Q(s,a)$最大的a。
这种方法也称为Q-Learning。