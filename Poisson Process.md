# k-PMF of a Given Period $\tau$
Bernoulli Process with continuous time.
![[截屏2025-08-26 15.49.54.png]]
![[截屏2025-08-26 15.49.01.png]]
![[截屏2025-08-26 15.51.32.png]]
# y-PMF of a Given k
![[截屏2025-08-26 16.10.44.png]]
Actually, it is $P(k-1,y)\cdot \lambda$
When k = 1, we have
$$
f_Y(y)=\lambda e^{-\lambda y}
$$
The same with exponential distribution, with
$$
E[y]=\frac{1}{\lambda}
$$
$$
var(y)=\frac{1}{\lambda^2}
$$
For random variables obey exponential distribution, we can show as:
$$
X\sim\text{exp}(\lambda)
$$
# Merging Poisson Process
![[截屏2025-08-26 16.17.52.png]]
For a given tiny period $\delta$,we have
$P(R\land G) = \lambda_1\delta\lambda_2\delta=0(\delta^2\,\,is\,\,too\,\,tiny)$
$P(R\land \lnot G)=\lambda_1\delta(1-\lambda_2\delta)=\lambda_1\delta$
$P(\lnot R\land G)=(1-\lambda_1\delta)\lambda_2\delta=\lambda_2\delta$
$P(\lnot R\land \lnot G)=(1-\lambda_1\delta)(1-\lambda_2\delta)=1-\lambda_1\delta-\lambda_2\delta$
Stay and see from the beginning, we have
$$
P(R\,\,comes\,\,first)=\frac{\lambda_1}{\lambda_1+\lambda_2}
$$
$$
P(G\,\,comes\,\,first)=\frac{\lambda_2}{\lambda_1+\lambda_2}
$$
# Splitting Poisson Process
In a time point, there is $\lambda\delta$ probability that the event occurs. $p$ change to a sub event, and $1-p$ change to another. 
Than, $\lambda_1=p\lambda\delta$,$\lambda_2=p\lambda\delta$.
![[截屏2025-08-27 11.24.34.png]]
# Random Incidence for Poisson
Given a running Poisson Process, and the exact time points that the event happens.
![[截屏2025-08-27 11.32.42.png]]
Choosing a uniform random time point, time to last event occurred is $T_1$, time to next event is $T_2$, we have
$$
T_1\sim exp(\lambda),T_2\sim exp(\lambda)
$$
Length of the chosen duration $T=T_1+T_2$, we have
$$
E[T] = E[T_1+T_2] = E[T_1]+E[T_2] = \frac{2}{\lambda}
$$
Bigger than $T_1$ and $T_2$, because larger duration is more likely to be chosen.
Actually, T is equal to the time needed to observe 2 arrivals in Erlang Distribution.
$$
P_T(t)=\lambda^2te^{-\lambda t}
$$