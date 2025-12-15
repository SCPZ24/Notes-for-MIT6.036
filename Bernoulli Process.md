# Definition
A sequence of independent Bernoulli trials, with success probability p and failure possibility 1-p.
# Attributes
## Memoryless, with discrete time.
## Inner Geometric Random Variable
Given T means number of trials until a first success occurs.
$$
E[T]=\frac{1}{p}
$$
$$
var(T)=\frac{1-p}{p^2}
$$
T is a Geometric Random Variable.
## Stacking Up
$Y_k$ means :after $Y_k$ trials, k successes occurs.
$$
E[Y_k]=kT=\frac{k}{p}
$$
$$
var[Y_k]=k\frac{1-p}{p^2}
$$
# Two types of Bernoulli Process
## Split
One Trial can be divided into two(or more) parts, generating two(or more) sequences.
The two(or more) parts can form two(or more) Bernoulli Process.
For example:
![[截屏2025-08-24 16.12.42.png]]
For A, the possibility of seeing one success trial is $qp$.
For B, it is $(1-q)p$.
## Merge
Two(or more) sequences yield one Bernoulli Process.
For example:
![[截屏2025-08-24 16.17.46.png]]
The uniform possibility of one trail is $p+q-pq$.