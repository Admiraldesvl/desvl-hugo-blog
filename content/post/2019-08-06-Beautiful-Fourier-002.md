---
title: "优美的Fourier级数（二）"
date: 2019-08-06
tags: [
    "数学分析", "Fourier分析"
]
categories: [
    "数学",
]
mathjax: true
comment: true
---

## 前言

如果你和Fourier级数打交道，那么在处理间断函数，特别是锯齿状函数的时候，有没有注意过间断处的形状？它为什么会处在中间位置？什么时候会出现这种情况？这就是接下来要解决的问题. 这期间会涉及到其他重要的基本技巧，还是那句话，Fourier级数绝对不仅仅是处理一系列三角函数. 还要注意，这里我们探讨的函数应该是局限在$[-\pi,\pi]$的实函数.

## Jordan判别法

> 如果$f$是有界差分，那么$$s_N(x)\to\frac{f(x^+)+f(x^-)}{2}$$, 其中$f(x^+)=\lim\_{h\to0^+}f(x+h)$, $f(x^-)=\lim\_{h\to0^+}f(x-h)$

### 有界差分
关于有界差分，可以看成推广的“弧长”. 在$[a,b]$上，$f(x)$的总差分的定义是这样：
\[
	T\_f(x):=\sup\\{\sum\_{i=1}^n|f(x\_i)-f(x\_{i-1})||a=x\_0<x\_1<\cdots<x\_n=x\\}
\]
对于连续函数来说，这就是$f(x)$在$[a,x]$的弧长. 而如果$f(x)$是$[a,b]$上的有界差分，那么只需要满足$T_f(b)<\infty$. 

注意到$f(x)$还可以写成

\[
	f(x)=\frac{1}{2}(T\_f(x)+f(x))-\frac{1}{2}(T\_f(x)-f(x))
\]

而$\frac{1}{2}(T\_f(x)+f(x))$和$\frac{1}{2}(T\_f(x)-f(x))$都是非负的单调增函数. 事实上，有界差分一定可以写成两个单调增函数的差，具体证明可以参见[这里](https://math.stackexchange.com/questions/141338/bounded-variation-difference-of-two-increasing-functions).

### 积分第二中值定理

> 如果定义在$[a,b]$上的实函数$f$和$g$满足$f$ 连续且$g$单调，那么存在$c\in(a,b)$使得\[\int\_a^bf(x)g(x)dx=g(a^+)\int\_a^cf(x)dx+g(b^-)\int\_c^bf(x)dx\]

这个定理的证明可以参见[这里](http://www.math.mcgill.ca/labute/courses/255w03/L9.pdf)，也可以用Abel变换进行证明.

### 回到Jordan判别法的证明

因为$D_N(x)$是偶函数，$S_N(x)$可以重写成
\[
	s_N(x)=\frac{1}{2\pi}\int\_0^{\pi}(f(x-t)+f(x+t))D_N(t)dt
\]

如果我们定义$g(t)=f(x+t)+f(x-t)$, 那么就有
\[
	g(0^+)=f(x^+)+f(x^-)
\]

原命题即证明
\[
	\frac{1}{2\pi}\int\_0^{\pi}g(t)D_N(t)dt\to\frac{g(0^+)}{2}
\]

又考虑到$g(t)$是有界差分，可以写成两个单调增函数的差. 那么这里只需要这个极限对单调增函数成立即可.

设有单调增函数$h(t)$, 定义$H(t)=h(t)-h(0^+)$; 注意到
\[
	\frac{1}{2\pi}\int\_0^{\pi}H(t)D\_N(t)dt\to\frac{H(0^+)}{2}=0
\]
当且仅当
\[
	\frac{1}{2\pi}\int\_0^{\pi}h(t)D\_N(t)dt\to\frac{h(0^+)}{2}
\]
这是因为$\frac{1}{2\pi}\int\_0^{\pi}D_N(t)dt=\frac{1}{2}$. 那么不失一般性，可以设$h(0^+)=0$, 那么需要证明，
\[
	\frac{1}{2\pi}\int\_0^{\pi}h(t)D\_N(t)dt\to 0\quad(N\to\infty)
\]

因为$h(0^+)=0$, 对任意$\varepsilon>0$, 有$\delta>0$使得对任意$x<\delta$有$g(x)<\varepsilon$. 原积分可以展开为
\[
    \frac{1}{2\pi}\int\_0^{\pi}h(t)D\_N(t)dt=\frac{1}{2\pi}\int\_0^{\delta}h(t)D_N(t)dt+\frac{1}{2\pi}\int\_{\delta}^{\pi}h(t)D_N(t)dt
\]

注意到最后一个积分可以写成
\[
    \frac{1}{2\pi}\int\_0^{\pi}\frac{h(t)}{\sin(t/2)}\chi\_{[\delta,\pi]}\sin(N+\frac{1}{2})tdt
\]

其中$\chi\_E=\begin{cases}1,x\in E\\\\\{0}, x\notin E\end{cases}$

那么这个积分的讨论就和上一篇里收敛性证明的最后利用Bessel不等式的推论的过程一样了，我们得到，这个积分的极限为0. 证明在这里略去. 

第一个积分的证明用到积分第二中值定理：
\begin{equation}
    \begin{aligned}
        \frac{1}{2\pi}\int\_0^{\delta}h(t)D_N(t)dt&=\frac{1}{2\pi}h(\delta^-)\int\_c^{\delta}D_N(t)dt\\\\\\
        &\leq\frac{\varepsilon}{2\pi}\int\_c^{\delta}D_N(t)dt
    \end{aligned}
\end{equation}

其中$0<c<\delta$. 如果我们能证出$\int\_c^{\delta}D_N(t)dt$是有界的，那么$\varepsilon\to0$时，就有所求结论. 注意到 
\[
    |\int\_c^{\delta}D_N(t)dt|\leq |\int\_c^{\delta}\sin(N+\frac{1}{2})t(\frac{1}{\sin(t/2)}-\frac{1}{t/2})dt|+|\int\_c^{\delta}\frac{\sin(N+\frac{1}{2})t}{t/2}dt|
\]
注意到$\frac{1}{\sin(t/2)}-\frac{1}{t/2}\to 0(t\to 0)$, 而这个函数在$(0,\pi]$上连续有定义，故$\frac{1}{\sin(t/2)}-\frac{1}{t/2}$在$[0,\pi]$上可积. 再利用Bessel不等式的推论，不等式右侧第一个积分趋近于0， 同时也是有界的.

针对另一个积分的讨论，我们首先令$y=(N+\frac{1}{2})t$, 那么能得到
\[
    \int\_c^{\delta}\frac{\sin(N+\frac{1}{2})t}{t/2}dt=2\int\_{(N+\frac{1}{2})c}^{(N+\frac{1}{2})\delta}\frac{\sin y}{y}dy
\]

这个积分的有界性可以通过探讨函数$y=\int\_0^{x}\frac{\sin x}{x}dx$得到.这里$x>0$. 通过很多办法可以发现，$\lim\limits_\{x\to\infty}y=\frac{\pi}{2}$. 具体可以参见[这里](https://math.stackexchange.com/questions/5248/evaluating-the-integral-int-0-infty-frac-sin-x-x-mathrm-dx-frac-pi).

考虑到$y'=\frac{\sin x}{x}$, $y$ 在$[2k\pi,(2k+1)\pi]$递增，在$[(2k-1)\pi,2k\pi]$递减. 现证明$y(\pi)$为函数的最大值. 

因为$y$在$[0,\pi]$递增，所以$0<x<\pi$时，$y(x)<y(\pi)$.

又考虑到
\[
    y((2k-1)\pi)-y((2k+1)\pi)=\int\_{(2k-1)\pi}^{(2k+1)\pi}\frac{\sin x}{x}dx
\]
而
\[
    \int\_{(2k-1)\pi}^{(2k+1)\pi}\frac{\sin x}{x}dx>\int\_{(2k-1)\pi}^{(2k+1)\pi}\frac{\sin x}{(2k+1)\pi}dx=0
\]
从而有
\[
    y(\pi)>y(3\pi)>\cdots>y((2k+1)\pi)
\]
而根据函数的单调性，一定有
\[
    \begin{cases}
        y(2k\pi)<y((2k-1)\pi)\\\\\\
        y(2k\pi)<y((2k+1)\pi)
    \end{cases}
\]
因此$y$的最大值为$y(\pi)$. 用类似的办法还可以发现$y(0)$为最小值. 这说明，$y$是有界的.

再回到原来的积分，有
\[
    2|\int\_{(N+\frac{1}{2})c}^{(N+\frac{1}{2})\delta}\frac{\sin y}{y}dy|=2|y((N+\frac{1}{2})\delta)-y((N+\frac{1}{2})c)|<2y(\pi)
\]

至此，我们证明了$\int\_c^{\delta}D_N(t)dt$是有界的. 进一步也得出了想要的收敛性的结论.

## 总结&其他想说的

至此，Jordan判别法得到了证明. 但千万不要认为，Fourier级数的收敛是这么简单的一件事情. 这可能会让人觉得，既然有界差分就有这么好的收敛现象，那么连续函数一定就收敛得更好. 但实际情况完全不一样：存在至少有一点发散的连续函数的Fourier级数（du Bois Reymond, 1873）. 此外，甚至存在每点都发散的Fourier级数(Kolmogorov, 1926). 这和处处连续但处处不可导的函数一样，很难想象，但是理论上确实存在. 

但是，Jordan判别法还是体现了Fourier级数的优美之处. 因为满足有界差分的函数还是很容易获得的.
