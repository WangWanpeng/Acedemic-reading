<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

		- [1. Problem Setting](#1-problem-setting)
		- [2. Stochastic dynamic model](#2-stochastic-dynamic-model)
		- [3. Base stock policy](#3-base-stock-policy)

<!-- /TOC -->

### 1. Problem Setting
A cash constrainted retailer, selling one item, stochastic demand, no fixed ordering cost, fully lost sales. <br>
Other parameters:

parameters  |  description
---|---
$p$  | price
$c$  | variable ordering cost
$\gamma (0\leq\gamma\leq c< p)$  |  salvage value  |
$S_n$  | initial cash at period $n$  |
$x_n$  | initial inventory at period $n$  |
$y_n$  | immediate inventory after replenishment  |
$S_{N+1}$  | terminal cash  |
|d   |interest rate   |

Cash constraint:
$$
c(y_n-x_n)\leq S_n
$$

### 2. Stochastic dynamic model
States: &nbsp;  $x_t$, $S_t$

States transitions function:
$$
\begin{aligned}
x_{n+1}=&~ (y_n-D_n)^+\\
S_{n+1}=&~S_{n}+p\min\{y_n, D_n\}+(1+d)(S_n-c(y_n-x_n))
\end{aligned}
$$

Optimality equation: define $V_n(x, S)$ as the maximum expected terminal cash for period $n$ given intial cash $S$ and initial inventory $x$.
$$
V_n(x,S)=\max_{x\leq y\leq x+S/c} V_{n+1}\big((y-D)^+, S+p\min\{y, D_n\}+(1+d)(S-c(y-x))\big)
$$

Boundary condition:
$$
V_{N+1}(x,S)=S+\gamma x
$$

### 3. Base stock policy

**Lemma 1**. $V_n(x,S)$ is non-decreasing for $S$ given fixed $x$.

This property is intuitive. The domain for decision variable $y$ is larger when $S$ is increasing and $x$ is fixed.

**Lemma 2**. $V_n(x-z, S+cz)$ or $V_n(x-z, S+pz)$ is non-decreasing for $z$ given fixed $x$ and $S$.

**Lemma 3**. $V_n(x, S)$ is jointly concave for $x$ and $S$ for any period $n$.

*Proof*:<br> We prove this by induction. Clearly, $V_n(x, S)$ is jointly concave when $n=N+1$. Assume $V_{n+1}(x, S)$ is jointly concave, we now prove this property for $n$. The domain:
$$
\mathbb C=\{(x, y, S)\mid x\geq 0, x\leq y\leq x+S/c, S\in\mathbb R\}
$$
can be easily proved to be a convex set. Based on the property that **minimizing a concave function in a convex set is also concave**, we need to prove $V_{n+1}()$ is jointly concave in $x$, $y$, $S$. Assume two points $(x_1, y_1, S_1)$, $(x_2, y_2, S_2)$, two parameters $\lambda$, $\overline{\lambda}$ ($\lambda+\overline{\lambda}=1, 0\leq \lambda, \overline{\lambda}\leq 1$).
$$
\begin{aligned}
&V_{n+1}\big((\lambda y_1+\overline{\lambda}y_2-D)^+,~~p\min\{\lambda y_1+\overline{\lambda}y_2, D_n\}+\dots\big)\\
=&V_{n+1}\big(\lambda y_1+\overline{\lambda}y_2-\min\{\lambda y_1+\overline{\lambda}y_2, D_n\},~~p\min\{\lambda y_1+\overline{\lambda}y_2, D_n\}+\dots\big)\\
\geq &V_{n+1}\big(\lambda y_1+\overline{\lambda}y_2-\lambda\min\{y_1, D_n\} -\overline{\lambda}\{y_2, D_n\},~~\lambda p\min\{ y_1, D_n\}+\overline{\lambda}p\{y_2, D_n\}+\dots\big)\\
\geq &\lambda V_{n+1}((y1-D_n)^+, p\min\{y, D_n\})+
\end{aligned}
$$
