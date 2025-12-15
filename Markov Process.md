# Definitions
![[截屏2025-10-02 02.31.36.png]]
## $X_n$
State after n transitions.
$X_0$: Initial state, can be either given or random.
## Property
The general possibility of transition from state i to state j
$$
p_{ij}=P(X_{n+1}=j|X_n=i)
$$
The general possibility of transition from state i to state j with n transitions.
For a given initial state i:
$$
r_{ij}(n)=P(X_n=j|X_0=i)
$$
By recursion, we have
$$
r_{ij}(n)=\sum_{k=1}^mr_{ik}(n-1)p_{kj}=\sum_{k=1}^mp_{ik}r_{kj}(n-1)
$$
# Recurrent and Transient States
Transitions(possibility to switch from a state to another) of a system can be represented by a Directed Graph.
![[截屏2025-10-02 02.40.47.png]]
## Recurrent
![[截屏2025-10-02 02.44.47.png]]
## Recurrent Class
![[截屏2025-10-02 02.43.47.png]]
"Communicate" means a way can be found from one vertical to another vertical in a directed graph.
## Transient
For states that are not recurrent, they are transient.
## Periodic Case
![[截屏2025-10-02 02.48.15.png]]
# Steady-State Probabilities
In a recurrent class, after plenty of transients, the possibility of landing on a given state is fixed(converge to a static value).
We use $\pi_i$ to represent the possibility to land on state i after enough steps.
$$
\pi_i = \lim_{n\rightarrow+\infty}r_{ki}(n)
$$
for which, $k$ is an initial state.
In terms of $\pi_i$, within a given recurrent class, $k$ does not matter.
## Linear Equations of $\pi$ Series
For a recurrent system with $n$ states, we have
$$
\pi_j = \sum_{k=1}^n\pi_kp_{kj}
$$
and
$$
\sum_{k=1}^n\pi_k=1
$$
## Transition Frequency
![[截屏2025-10-02 02.59.28.png]]
# Birth-death Process
## Definition
States in a Birth-death process a linked like a chain.
A state can only transfer to two neighbor states and itself.
![[截屏2025-10-02 03.01.56.png]]
It is like a process of Accumulate-Consume balancing, for example, number of users on the server(state i means i users online).
## Balance Equation
In a long term perspective, we can believe that frequency of transfer from state n to state n+1 is equal to that of transfer back from state n+1 to state n.
![[截屏2025-10-02 03.06.28.png]]
So we have
$$
\pi_ip_i=\pi_{i+1}p_{i+1}
$$
## Special Case
![[截屏2025-10-02 03.07.07.png]]
# Absorption Probabilities
## Definition
If there are transient cases in a system, after running enough steps, the possible states will collapse to a certain part(recurrent class) of the whole system.
![[截屏2025-10-02 03.13.18.png]]
In system in the graph above, it's bound to fall in the state shown on the top or right of the image.
## Expected Time to Absorption
The number of steps that is expected to need to fall trapped is dependent on the initial state.
We use $\mu_i$ to represent the steps needed to be trapped(no matter be trapped in which part) with the initial state i.
If it borns in a already trapped state i, then we have
$$
\mu_i = 0
$$
for other cases, after taking a step to another state from initial state, we update the $\mu_i$.
So we have
$$
\mu_i = 1 + \sum_{k=1}^np_{ik}\mu_k
$$
So, we have a System of Linear Equations(线性方程组), with a unique solution.
# Mean First Passage and Recurrence Times
## Definition of Mean First Passage
Given a target state $s$, we want to know the steps need to get to $s$ for the first time.
$$
t_i = E[min(n\geq1\,\,that\,\,X_n=s)|X_0 = i]
$$
## Unique Solution
![[截屏2025-10-02 03.41.49.png]]
## Mean Recurrence Time
![[截屏2025-10-02 03.45.19.png]]