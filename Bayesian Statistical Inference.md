Sometimes we need to use Methods we've learned to solve practical problems.
We need to detect input info $\Theta$. But usually our detector has some noise $N$. So, given an original input $\Theta$, we may get a detected value $X$.
Then, we have a Estimator which decodes $X$ then gives us back an estimated $\widehat{\Theta}$.
![[截屏2025-10-07 13.08.45.png]]
Notice that $\Theta$ and $X$ is not always a number but can be a vector.
Suppose we have distribution of $\Theta$ and $X$ for any $P_{X,\Theta}(x,\theta)$, with our input X, we can get a certain $P_{\Theta|X}(\theta|x)$ using Bayesian rules.
For discrete cases
$$
p_{\Theta|X}(\theta|x)=\frac{P_\Theta(\theta)p_{X|\Theta}(x|\theta)}{p_X(x)}
$$
and
$$
p_X(x)=\sum_\theta p_\Theta(\theta)p_{X|\Theta}(x|\theta)
$$
For continuous cases
$$
p_{\Theta|X}(\theta|x)=\frac{P_\Theta(\theta)f_{X|\Theta}(x|\theta)}{f_X(x)}
$$
and
$$
p_X(x)=\int f_\Theta(\theta)p_{X|\Theta}(x|\theta)d\theta
$$
# Maximum A Posteriori Estimation(MAP)
For a $X$, we iterate through all $\theta$, then get a PMF or PDF for $p_{\Theta|X}(\theta|x)$.
![[截屏2025-10-07 13.29.04.png]]
Then we find the $\theta$ that maximizes $p_{\Theta|X}(\theta|x)$.
So we get a certain estimate outcome $\theta^*$ based on MAP.
However, for some biased cases, MAP can be misleading.
# Least Mean Squares Estimation(LMS)
If we have a constant $c$, we define that the Squared Error of the estimated value is $E[(\Theta-c)^2|X=x]$. Here, $\Theta$ is a random variable.
It turns out that the mean of the $\theta$ PDF or PMF minimizes the Squared Error.
So take $c = E[\Theta|X=x]$.
Moreover we have
$$
E[(\Theta-E[\Theta|X=x])^2|X=x]=Var(\Theta|X=x)
$$
Briefly, for any function $g(X)$, we have
![[截屏2025-10-07 13.40.36.png]]
So $\widehat{\Theta}=E[\Theta|X]$ can be chosen as the estimate outcome.
Let random variable $\Theta$ be the real input, and $\widehat{\Theta}$ be out estimate outcome.
The Estimation Error is
$$
\tilde{\Theta}=\widehat{\Theta}-\Theta
$$
We have
$$
E[\tilde{\Theta}|X=x]=0
$$
$$
E[\tilde{\Theta}]=0
$$
for any function $h(X)$
$$
E[\tilde{\Theta}h(X)]=0
$$
because $h(X)$ is constant.
$$
cov(\tilde{\Theta},\widehat{\Theta})=0
$$
# Linear LMS
Different to LMS, Linear LMS needs to find a overall $\tilde{\Theta} = aX + b$ that minimizes $E[(\Theta-aX-b)^2]$.
Then we can get the optimized $\Theta$ immediately with an detected $X$.
In fact, it's just the process if finding parameter $a$ and $b$.
By taking derivatives, we find the best $\Theta$ is
$$
\tilde{\Theta}_L=E[\Theta]+\frac{cov(X,\Theta)}{var(X)}(X-E[X])
$$
## Multiple Data Cases
Observing multiple $X$, we have estimate form
$$
\tilde{\Theta}=a_1X_1+a_2X_2+......+a_nX_n+b
$$
The solution is also taking derivatives and solve the linear system.
And sometimes, we can do some Non-linear transformations to our observed datas/
![[截屏2025-10-07 14.06.24.png]]