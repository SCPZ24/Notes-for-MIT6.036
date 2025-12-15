# Probability Density Function(PDF)
## Definition
![[Pasted image 20250801232239.png]]
## Attributes
![[Pasted image 20250801232340.png]]
# Cumulative Density Function(CDF)
![[Pasted image 20250801232518.png]]
Some circumstances may contain both Continuous Distribution and Discrete Distribution.
e.g. Playing a game where one has 1/2 possibility to get score 1/2. For the left circumstances, play another game where he has equal possibility to get any value between 0 and 1.Following is the PDF&PMF diagram and the CDF diagram.
![[Pasted image 20250801232610.png]]
# Intro to Normal Distribution
![[Pasted image 20250801233051.png]]
![[Pasted image 20250801233108.png]]
Mean and Standard Deviation of Normal Distribution is linear.
$Let\,Y=aX+B,then$
$$
\begin{matrix}E[Y]=aE[X]+B\\Var(Y)=a^2\sigma^2\\\sigma(Y)=a\sigma\end{matrix}
$$
# Multi Variables
## Definition
![[Pasted image 20250804210644.png]]
![[Pasted image 20250804212043.png]]
$$
f_X(x)=\int_{-\infty}^{+\infty}f_{X,Y}(x,y)dy
$$
![[Pasted image 20250804212537.png]]
$$
Else\,\,Independent\,\,if:P(x\in A,y\in B)=P(x\in A)\cdot P(y\in B)
$$
![[Pasted image 20250804212817.png]]
If random variables A and B are independent, then:
$$
E(AB) = E(A)\cdot E(B)
$$
## Bayes Rules
![[Pasted image 20250804213146.png]]
![[Pasted image 20250804213203.png]]
# Derived Distribution
## Use CDF to calculate PDF
For some models, we can research their CDF instead of PDF.
$F_X(x)$ is CDF while $f_X(x)$ is PDF. For a fixed model, we have
$$
f_Y(y)=\frac{dF_Y}{dy}(y)
$$
![[Pasted image 20250804213848.png]]
## Functional
![[Pasted image 20250819164742.png]]
Using the equation above, given PDF of X and the function Y = g(X), we can calculate the PDF of Y.
**Example**
![[Pasted image 20250820001344.png]]
![[IMG_7805.jpg]]
# Convolution
Let W = X + Y, where X , Y are independent random variables, with each a given PDF.
We can convolve the PDF of W.
$$
f_W(w)=\int_{-\infty}^{+\infty}f_X(x)f_Y(w-x)dx
$$
Two random variables which obey normal distribution are convolved, the outcome W also obeys normal distribution.
For example:
![[Pasted image 20250819165646.png]]
# Covariance(协方差)
## Definition
$$
cov(X,Y)=E[(X-E(X))\cdot (Y-E(Y))]=E[XY]-E[X]\cdot E[Y]
$$
## Attributes
$$
cov(X,X)=var(X)
$$
$$
var(X+Y)=2\cdot cov(X,Y)+var(X)+var(Y)
$$
$$
cov(X,Y)=cov(Y,X)
$$
for constants a and b , we have
$$
cov(aX,bY) = a\cdot b \cdot cov(X,Y)
$$
$$
cov(X+Y,Z)=cov(X,Z)+cov(Y,Z)
$$
if X and Y are independent, we have
$$
cov(X,Y)=0
$$
for the inverse case(given $cov(X,Y)=0$), we can only know X and Y are linearly independent. For example, $X$ ~ $N(0,1)\,\,and\,\,Y = X^2$,we have $cov(X,T)=0$ but X and Y have some relationship.
# Correlation Coefficient
## Definition
$$
\rho = E[\frac{X-E(X)}{\sigma_X}\cdot\frac{Y-E[Y]}{\sigma_Y}]=\frac{cov(X,Y)}{\sigma_X\cdot \sigma_Y}
$$
## Attributes
![[Pasted image 20250819232428.png]]
# Conditional Exceptions
$$
E[X|Y=y]=\sum_xxp_{X|Y}(x|y)
$$
$$
E[E[X|Y]]=\sum_yE[X|Y=y]p_Y(y)=E[X]
$$
$$
var(X)=E[var(X|Y)]+var(E[X|Y])
$$
