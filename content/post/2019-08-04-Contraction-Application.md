---
author: "Desvl"
date: 2019-08-04
title: "收缩定理和其应用"
tags: [
    "数学分析",
]
categories: [
    "数学",
]
mathjax: true
comment: true
--- 
## 什么是收缩

收缩的准确描述是这样的：

> 取度量空间$X$，度量$d$，函数$\varphi$是$X$到本身的映射，且满足$$d(\varphi(x),\varphi(y))\leq cd(x,y)$$. 其中$x,y\in{X}$, $c<1$. 那么$\varphi$就是一个从$X$到本身的收缩.

一个最简单的例子是， $y=\frac{x}{2}$. 这是一个“平缓”的函数。平缓的程度是怎样呢？斜率小于1. 

而收缩定理指出，对于这个函数，有且仅有一个$x$使得$\varphi(x)=x$. 例如上面的例子，只有$0=0$这一个点. 接下来要给出证明. 这个证明方法在求极限时也非常实用，只要能构建出这样的收缩.

## 收缩的证明

任取$x_0\in{X}$, 按照如下方法定义数列$x_n$: 

$$x_{n+1}=\varphi(x_n)$$

从而会有

\[d(x_2,x_1)=d(\varphi(x_1),\varphi(x_0))\leq cd(x_1,x_0)\]

推广下去，就有

\[d(x_{n+1},x_n)\leq c^nd(x_1,x_0)\]

对于$n<m$, 就有
\begin{equation}
    \begin{aligned}
        d(x\_n,x\_m)\leq\sum\_{i=n+1}^m d(x\_i,x\_{i+1})\leq(c^n+c^{n+1}+\cdots+c_{m-1})d(x_1,x_0)\leq\frac{c^n}{1-c}d(x\_1,x\_0)
    \end{aligned}
\end{equation}
这说明，$x_n$是一个Cauthy数列，又考虑到$X$是完备空间，因此$x_n$收敛. 设$x_n$的极限为$x$. 由收缩的定义可知，$\varphi$为一致连续的函数，从而有
\[
    \varphi(x)=\lim\limits\_{n\to\infty}\varphi(x\_n)=\lim\limits\_{n\to\infty}x\_{n+1}=x
\]
至于唯一性的证明，可设$\varphi(x)=x$, $\varphi(y)=y$. 从而有$d(\varphi(x),\varphi(y))=d(x,y)\leq cd(x,y)$ 这只有在$d(x,y)=0$时成立. 唯一性得到证明.

## 简单应用
下面是一道数学专业研究生入学考试题。可以发现，利用“压缩”这个工具，问题的解决变得非常简单.

> 已知$0\leq a\leq 1, b \geq2$, 有数列$\{x\_n\}$ 满足x_0=0, 且有递推关系\[x\_{n+1}=x\_n-\frac{1}{b}(x\_n^2-a),\]求证此数列收敛，并求出极限.

_在这里设$\phi(x)=x-\frac{1}{b}(x^2-a)$， 那么有$x\_{n+1}=\varphi(x\_n)$. 如果能证出$\varphi$为一个压缩，极限的问题就迎刃而解了._

**证明**

设$\varphi(x)=x-\frac{1}{b}(x^2-a)$. 则$x\_{n+1}=\varphi(x\_n)$. 在这里$x\_1=\varphi(x\_0)=\frac{a}{b}$. 现证明对所有$n>0$ 有$\frac{a}{b}\leq x\_n\leq 1$, 对$n$进行归纳.

$n=1$时，不等式已成立.

假设$n=k$时成立，则$n=k+1$时，有
\[
    x\_{k+1}=\frac{a}{b}-\frac{bx\_k-x\_k^2}{b}
\]
考虑到$y=bx-x^2$在$[\frac{a}{b},\frac{b}{2}]$单调递减，而$\frac{b}{2}\geq1$, 故有
\[
    x\_{n+1}\leq\frac{a}{b} +\frac{b-1}{b}\leq 1
\]
而$y(\frac{a}{b})\geq y(0)=0$, 故$x\_{n+1}\geq\frac{a}{b}$.

因此不等式对所有$n>0$成立.

利用这个不等式，得到
\[
    |f(x)-f(y)|=|x-y||1-\frac{x+y}{b}|\leq|x-y||1-\frac{2a}{b^2}|, \quad \frac{a}{b}\leq x,y \leq 1
\]

$a=0$时，得到$x\_1=x\_2=\cdots=0$, 故极限存在且为0.

$a\neq 0$时，令$c=|1-\frac{2a}{b^2}|$, 则始终有$c<1$. 此时就是上文中所提到的压缩. 收敛的证明略去.

设$\lim\limits\_{n\to\infty}x_n=x$, 则$x=\varphi(x)$. 解得$x=\sqrt{a}$. 这在$a=0$时也成立.

综上，$\lim\limits\_{n\to\infty}x_n$存在，且值为$\sqrt{a}$.

## 总结

压缩是非常有实用价值的工具. 利用它我们可以解决这种函数、数列的极限问题，但它的用途并不局限一元实数函数. 这也是为什么在定义的时候指出是度量空间和指定的度量. 例如，在$\mathbb{R}^n$中证明隐函数定理，就涉及到它的直接利用.

## 关于度量

度量函数$d(x,y)$即表示两点之间的距离，满足以下三个条件：

- $d(x,y)=0$当且仅当$x=y$.

- $d(x,y)=d(y,x)$.

- $d(x,y) + d(y,z) \leq d(x,z)$ (三角形不等式)

而度量空间即一个有度量函数的集合. 一个简单的例子是，全体实数$\mathbb{R}$, 度量函数$d(x,y)=|x-y|$.
