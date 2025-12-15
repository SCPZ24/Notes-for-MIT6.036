# Weak Law of Large Numbers
## Chebyshev's Inequality
For a random variable $X$ with mean $\mu$ and variance $\sigma^2$, we have
$$
\int_{-\infty}^{\mu-c}f_X(x)dx+\int_{\mu+c}^{+\infty}f_X(x)dx=P(|x-\mu|\geq c)
$$
and for $x\in(-\infty,\mu-c)$ and $x\in(\mu+c,+\infty)$, we have
$$
(x-\mu)^2 \geq c^2
$$
So there are
![[截屏2025-10-02 22.12.38.png]]
So, we have Chebyshev's Inequality
$$
P(|X-\mu|\geq c) \leq \frac{\sigma^2}{c^2}
$$
and
$$
P(|X-\mu|\geq k\sigma)\leq \frac{1}{k^2}
$$
which indicates that margin values(far away from mean) have smaller possibility to meet.
## Convergence in Probability(概率的收敛)
$Y_1,Y_2,Y_3,......,Y_n,......$ is a sequence of random variables.
If for every $\epsilon > 0$, we have
$$
\lim_{n\rightarrow+\infty}P(|Y_n-a|\geq\epsilon)=0
$$
then we can say: $Y_n$ converges to constant a.
Convergence can't tell about the mean and variance of $Y_n$.
## Convergence of the Sample Mean
$X,X_1,X_2,X_3,......,X_n$ is random variables formed in same way, which have mean $\mu$, variance $\sigma^2$
Let
$$
M_n = \frac{\sum_{i=1}^nX_i}{n}
$$
So
$$
E[M_n]=\mu
$$
$$
Var(M_n)=\frac{\sigma^2}{n}
$$
And we have
$$
P(|M_n-\mu|\geq\epsilon)\leq\frac{Var(M_n)}{\epsilon^2}=\frac{\sigma^2}{n\epsilon^2}
$$
As $n\rightarrow+\infty$, $(|M_n-\mu|\geq\epsilon)\rightarrow0$.
So, $M_n$ converges in probability to $\mu$.
## Standard Scaling of $M_n$
Let
$$
S_n = \sum_{i=1}^nX_i
$$
And
$$
M_n=\frac{S_n}{n}
$$
So,$Var(M_n)=\frac{\sigma^2}{n}$.
Let
$$
D_n=\frac{S_n}{\sqrt{n}}
$$
Then, $D_n$ have constant variance
$$
Var(D_n)=\sigma^2
$$
# Central Limit Theorem
$X_1,X_2,X_3,X_4,......,X_n$, a sequence of random variables with identical distribution.
Let $S_n=\sum_{i=1}^nX_i$. Then, we standardize it.
Let
$$
Z_n = \frac{S_n-E[S_n]}{\sigma_{S_n}} = \frac{S_n-nE[X]}{\sqrt{n}\sigma}
$$
Let Z be a normal random variable that have $Z\sim N(0,1)$.
If n is large enough(usually 18-30; if the pdf of $X$ is symmetry, the needed n can be smaller), for any constant $c$, we have
$$
P(Z_n\leq c)\rightarrow P(Z\leq c)
$$
In an another word, CDF of $Z_n$ converges to that of $Z$.
Approximately, we can say $Z_n$ and $S_n$ is normal.
