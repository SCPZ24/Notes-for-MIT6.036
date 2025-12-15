# Random variable
![[Pasted image 20250720221501.png]]
# Probability Mass Function(PMF)
## Definition
$$
p_X(x)=P(X=x)
$$
$$
\begin{matrix}p_X(x)\geq 0\\\sum_xp_X(x)=1\end{matrix}
$$
## Binominal PMF
$$
p_X(k)=C_n^kp^k(1-p)^{n-k}
$$
# Expectation
## Definition
$$
E[X]=\sum_xxp_X(x)
$$
## Properties
$$
E[g(X)]=\sum_xg(x)p_X(x)
$$
$$
Statement\,\,E[g(X)]=g(E[X])\,\,is \,\,True\,\,only\,\,if\,\,it's\,\,Linear
$$
$$
E[\alpha X+B]=\alpha E[X]+\beta
$$
$$
E[X-E[X]]=0
$$
# Variance
## Definition
$$
var(X)=E[(X-E[X])^2]=E[X^2]-(E[X])^2
$$
## Properties
$$
var(X)\geq 0
$$
$$
var(\alpha X+\beta)=\alpha^2var(X)
$$
## Standard Deviation
$$
\sigma_X=\sqrt{var(X)}
$$
# Conditional PMF and Expectation
## Definition
$$
p_{X|A}(x)=P(X=x|A)
$$
$$
E[X|A]=\sum_xxp_{X|A}(x)
$$
![[Pasted image 20250720225017.png]]
## Geometric PMF
Do a experience constantly, there's possibility p that it gets probable outcome. X is the number that how many times the experience has been taken place until a first probable outcome happens.
![[Pasted image 20250720230711.png]]
Proof:
![[Pasted image 20250720230851.png]]
$$
in\,\,which\,\,P(X>0) = 1-p;P(X=1)=p;E[X|X=1]
$$
$$
E[X|X>1]=E[X|X-1>0]=E[X-1|X-1>0]+E[1|X-1>0]=E[X]+1
$$
Actually, we have$E[X-m|X-m>0]=E[X]$,according to the property of Geometric PMF.
# Multiple Random Variables
## Definition
![[Pasted image 20250720232059.png]]
## Independence
![[Pasted image 20250720232220.png]]
## Expectations
![[Pasted image 20250730005714.png]]
## Variances
![[Pasted image 20250730010715.png]]
## Examples in Thinking About Means And Variances
![[Pasted image 20250730010645.png]]
