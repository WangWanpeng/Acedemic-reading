<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

		- [1. Problem Setting](#1-problem-setting)
		- [2. Stochastic dynamic model](#2-stochastic-dynamic-model)
		- [3. Base stock policy](#3-base-stock-policy)
		- [4. Boundary for  $a^\ast$](#4-boundary-for-aast)
		- [5. Separating $S$ and $y$.](#5-separating-s-and-y)

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
V_n(x,S)=\max_{x\leq y\leq x+S/c} E\left\{V_{n+1}\big((y-D)^+, p\min\{y, D_n\}+(1+d)(S-c(y-x))\big)\right\}
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
\geq &\lambda V_{n+1}\big((y_1-D_n)^+, p\min\{y_1, D_n\}^+\big)+\overline{\lambda}V_{n+1}\big((y_2-D_n)^+, p\min\{y_2, D_n\}^+\big)
\end{aligned}\\
\hspace 350pt\Box
$$
The first inequality follows from Lemma 2, and the second inequality follows from the concavity of $V_{n+1}$.

**Theorem 1**. By the concavity of optimality equation, with fixed $S$, there exits an optimal base-stock level $y^\ast(S)$, the optimal ordering policy is:
* if $y^\ast\geq x+S/c$, use up all the cash to order.
* if $y^\ast< x+S/c$ and $x<y^\ast$, order up to $y^{\ast}$.
* if $x\geq y^\ast$, do not order.

### 4. Boundary for  $a^\ast$
Although the optimal policy for this problem is clear, how to compute the value of inventory controlling paramter $y^\ast$ is also important. Since optimality equation is complex, we should try to separate $y$ and $R$. Define another recursive equation:
$$
\begin{cases}
G_n(y)&= (1+d)^{N-n}\big[(p-c)\min\{y, D\}-dcy\big]+G_{n+1}(\max\{(y-D)^+, a_{n+1}^\ast\})\\
G_{N+1}(y)&=(\gamma-c)y &
\end{cases}
$$

**This equation can be viewed as the expected cash increment for period $n$ without cash constraint**. $a^{\ast}_n$ is the optimal $y$ for $G_n(y)$ and $a^{\ast}_{N+1}=0$. We can get a property for $a^\ast_n$.

When $n=N$,
$$
G_N(y)=(p-c)\min\{y, D\}-dcy+(\gamma-c)y
$$

It is concave. Threfore, $a^\ast_N=F^-(\frac{p-(1+d)c}{p-\gamma})$.

Try to get the first derivative of $G_n(y)$:
$$
G'_n(y)=\frac{\partial G_n(y)}{\partial y}=(1+d)^{N-n}\big[(p-c-dc)-(p-c)F(y)\big]+G_{n+1}'(y-D)\Pr(y-D\geq a^\ast_{n+1})
$$

Second derivative of $G_n(y)$ is:
$$
\frac{\partial^2 G_n(y)}{\partial^2 y}=-(p-c)f(y)+G_{n+1}''(y-D)\Pr(y-D\geq a^\ast_{n+1})
$$

Assume $G''_{n+1}$ is concave, $G_n(y)$ is concave by induction. When $y=a^\ast_{n+1}$, $G'_n(y)>0$. So, $a_n^\ast>a_{n+1}^\ast$. When $y=F^-(\frac{p-(1+d)c}{p-c})$, the first term of $G'_n(y)$ is zero, while the second term is always non-positive. So $a^\ast_n\leq F^-(\frac{p-(1+d)c}{p-c})$. By induction, we can get:
$$
F^-(\frac{p-(1+d)c}{p-c})\geq a_1^\ast\geq\dots\geq a_N^\ast=F^-(\frac{p-(1+d)c}{p-\gamma})
$$

### 5. Separating $S$ and $y$.

In order to compute $S^\ast$, we must separate $S$ and $y$ in the optimality equation. The most finding in this paper is:

**Theorem 2**.
* When $S\geq c(a_{n+1}^\ast-x)$ and $y\leq x+S/c$, the optimality euqation can be decomposed as:
*
$$
\pi_n(y, S)=(1+d)^{N-n+1}(S+cx)+G_n(y)
$$
* if $S\geq c(a_n^\ast-x)$, then $y_n^\ast(S)=a_n^\ast$; if $S<c(a_n^\ast-x)$, $y_n^\ast(S)>x+S/c$.

*Proof*:<br> By induction. When $n=N$,
$$
\begin{aligned}
\pi_N(x, S)=& p\min\{y, D\}+(1+d)(S-c(y-x))+\gamma (y-D)^+\\
=& (p-c)\min\{y, D\}+(1+d)(S+cx)-dcy+(\gamma-c)y\\
=& (1+d)(S+cx)+G_N(y)
\end{aligned}
$$

So Theorem 2 is valid for $N$. Assume it is valid for $n+1$, now we prove for $n$. For easiness, let $R=S+cx$ and define another equaiton
$$
\begin{aligned}
\tilde{V}_n(x,R)=&V_n(x, R-cx)\\
=&\max_{x\leq y\leq R/c}E\left\{V_{n+1}\big((y-D)^+, p\min\{y, D_n\}+(1+d)(S-c(y-x))\big)\right\}
\end{aligned}
$$

Therefore,
$$
V_n(x, S)=\max_{x\leq y\leq x+S/c}\pi_n(y, S)
$$
$$
V_{n+1}(x, S)=\max_{x\leq y\leq x+S/c}\pi_{n+1}(y, S)
$$

$\pi_n(y, S)$ is also jointly concave. By Theorem 1,
$$
V_{n+1}(x, S)=\begin{cases}
\pi_{n+1}(S/c+x, S)\quad &x+S/c< y_{n+1}^\ast(S), \\
\pi_{n+1}(y^\ast, S) & x<y_{n+1}^\ast(S)\leq x+S/c\\
\pi_{n+1}(x, S) &x\geq y_{n+1}^\ast(S)
\end{cases}
$$

By the inducting assumption,

(a) if $S\geq 0\geq c(a^\ast_{n+1}-x)$, then $y_{n+1}^\ast(S)=a_{n+1}^\ast$ and $x\geq a_{n+1}^\ast$, so
$$V_{n+1}(x, S)=\pi_{n+1}(x, S)=(1+d)^{N-n+1}(S+cx)+G_n(x)$$

(b) if $S\geq c(a^\ast_{n+1}-x)\geq 0$, then $y_{n+1}^\ast(S)=a_{n+1}^\ast$,
$$V_{n+1}(x, S)=\pi_{n+1}(y^\ast, S)=(1+d)^{N-n+1}(S+cx)+G_n(y^\ast)$$

(c)  if $c(a^\ast_{n+2}-x)\leq S<c(a^\ast_{n+1}-x)$, then $y^\ast>x+S/c$,
$$V_{n+1}(x, S)=\pi_{n+1}(S/c+x, S)=(1+d)^{N-n+1}(S+cx)+G_n(S/c+x)$$

(d) if $S<c(a^\ast_{n+2}-x)$, then $y^\ast>x+S/c$
$$V_{n+1}(x, S)=\pi_{n+1}(S/c+x, S)$$

Rewrite the cases as follows,
$$
V_{n+1}(x, S)=\begin{cases}
\pi_{n+1}(S/c+x, S)\quad & S+cx<ca^\ast_{n+2}\\
(1+d)^{N-n}(S+cx)+G_n(S/c+x) & ca^\ast_{n+2}\leq S+cx<ca^\ast_{n+1}\\
(1+d)^{N-n}(S+cx)+G_n(x) &ca^\ast_{n+1}\leq cx\leq S+cx\\
(1+d)^{N-n}(S+cx)+G_n(a_{n+1}^\ast) &cx\leq ca^\ast_{n+1}\leq S+cx
\end{cases}
$$

Therefore, when $S+cx>ca^\ast_{n+1}$ and $y\leq x+S/c$,
$$V_{n+1}(x,S)=(1+d)^{N-n+1}(S+cx)+G_n(\max\{x, a_{n+1}^\ast\})$$

So, when $S+cx>ca^\ast_{n+1}$, $p\min\{y, D\}+(1+d)(S+cx)-dcy\geq ca^\ast_{n+1}$
$$
\begin{aligned}
\pi_{n}(x, S)=&E\{V_{n+1}((y-D)^+, p\min\{y, D\}+(1+d)(S+cx)-(1+d)cy\}\\
=& (1+d)^{N-n}\big[p\min\{y, D\}+(1+d)(S+cx)-(1+d)cy\big]+G_n(\max\{(y-D)^+, a_{n+1}^\ast\})\\
=& (1+d)^{N-n+1}(S+cx)+(1+d)^{N-n}\big[p\min\{y,D\}-(1+d)cy\big]+G_n(\max\{(y-D)^+, a_{n+1}^\ast\})\\
=& (1+d)^{N-n+1}(S+cx)+G_n(y)
\end{aligned}
$$

And, when $S+cx\geq ca^\ast_{n+1}$, $y^\ast=S/c+x$.

Now, **let's prove that when $S+cx\leq ca^\ast_{n+1}$, $y^\ast=S/c+x$**. We must prove this by its first derivative and adopting convexity. Let $R=S+cx$. Recall that
$$
\pi_n(y, S)=E\left\{V_{n+1}\big((y-D)^+, p\min\{y, D_n\}+(1+d)(S-c(y-x))\big)\right\}
$$

Let $V_{n,1}(x, R)$ and $V_{n,2}(x, R)$ represent the partial derivatives with respect to $x$ and $R$, respectively. So,
$$
\begin{aligned}
\frac{\partial V_{n+1}(x, S)}{\partial y}
=&
\left[\int_0^y V_{n+1}()f(z)dz\right]'+\left[\int_y^\infty V_{n+1}()f(z)dz\right]'\\
=& V_{n+1}()f(y)-V_{n+1}()f(y)+V_{n+1}'()F(y)+V'_{n+1}()(1-F(y))\\
=& \int_0^y V_{n+1, 1}(y-z, pz+(1+d)(S-c(y-x))f(z)dz\\
&+
\end{aligned}
$$
