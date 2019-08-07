---
title: "优美的Fourier级数（一）"
date: 2019-08-05
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

Fourier级数是相当优美的一类级数，但它涉及到的问题绝对不仅仅是通过各种运算技巧求表达式. 相反，它是一个很复杂、很困难的大话题. 我在这里会把一些基本内容和一系列严格的证明整理下来. 从Fourier级数出发，我们能看到很多重要的基本技巧的应用，也会涉及和实际应用息息相关的问题. 当然这些内容里不会包括如何求表达式，我觉得计算机做得比我会好多了.

## Fourier级数

### 级数的表达
最常见的Fourier级数是这种形式：
\[
    f(x)=a\_0+\sum\_{n=1}^{\infty}(a\_n\cos nx+b\_n\sin nx)\quad x\in\mathbb{R}
\]

这里的$a\_n$和$b\_n$既可以是实数又可以是复数(但我们接下来主要讨论实数函数$f$). 有的地方把第一项写成$\frac{a_0}{2}$, 这是考虑到积分时会多出来的一个$\frac{1}{2}$. 两种写法单纯是如何统一表达，在后面会解释. 考虑到$e^{ix}=\cos x+i\sin x$, 上面的式子可以写成
\[
    f(x)= \sum\_{-\infty}^{\infty}c\_ne^{inx}\quad x\in\mathbb{R}
\]

用这种表达方式时不用考虑$c\_n$的细节. 注意到$a\_0$可以写成$a\_0\cos 0x + b_0\sin 0x$.

### 关于级数的系数，即函数的“坐标”

#### 单位正交系
我们先回忆线性代数里的知识. 一个行向量和一个列向量的乘积是这样的：

\begin{equation}
    \begin{bmatrix}a&b\end{bmatrix}\begin{bmatrix}c\\\\d\end{bmatrix}=ac+bd
\end{equation}
进一步，第一个行向量可以看成列向量的转置. 那么这个$ac+bd$就是两个2维平面内列向量的内积. 这即高中数学中所讲的“向量乘法”. 这涉及到经典欧基里德空间的内积定义. 而谈到向量，单位正交向量肯定是非常有探讨价值的. 因为一般情况下其他向量可以用单位正交向量比较简单地表示出来. 但是向量内积不仅仅存在于经典的欧氏空间. 我们可以定义一系列定义域相同的函数，例如函数$f$和$g$的内积可以定义成
\[
    (f,g)=\int\_a^b f(x)\overline{g}(x)dx
\]
其中$\overline{g}$表示$g$的共轭复数. 一个共轭一个不共轭可以和经典欧氏空间里一个转置一个不转置相类比.

在任何欧基里德空间里（对函数的定义也是欧基里德空间，区分于经典欧基里德空间），两个向量的内积为0, 说明两个向量正交，夹角为$\frac{\pi}{2}$. 而向量的模的平方即自身和自身的内积. 根据以上结果，我们可以定义函数的“单位正交系”. 若定义在$[a,b]$上的一系列函数$\{\varphi\_n(x)\}$满足$(\varphi\_n,\varphi\_n)=1$而$(\varphi\_n,\varphi\_m)=0(m\neq n)$, 则称为单位正交系.

#### 再看Fourier级数

可以验证，在$[-\pi,\pi]$上，下列两组函数是单位正交的：
\[
    \frac{e^{ix}}{\sqrt{2\pi}},\frac{e^{2ix}}{\sqrt{2\pi}},\frac{e^{3ix}}{\sqrt{2\pi}},\cdots
\]
\[
    \frac{1}{\sqrt{2\pi}},\frac{\cos x}{\sqrt{\pi}},\frac{\sin x}{\sqrt{\pi}}, \frac{\cos 2x}{\sqrt{\pi}},\cdots
\]

读到这里可以发现，$a\_0$和$\frac{a\_0}{2}$的表示应该和$\frac{1}{\sqrt{2\pi}}$或者$\frac{1}{\sqrt{\pi}}$有关.

在$\mathbb{R}^n$里，如果知道单位正交向量$\mathbf{e\_1},\cdots,\mathbf{e\_n}$, 那么任意向量都可以唯一表示成$x\_1\mathbf{e\_1}+\cdots+x\_n\mathbf{e\_n}$. 这在其他欧氏空间里也是一样的. 向量$\mathbf{\alpha}$在的第$k$坐标分量为$(\mathbf{\alpha},\mathbf{e\_k})$. 通过这个角度看Fourier级数，就会发现，各项的系数就是函数的坐标：
\[
    c\_m=\int_a^b f(x)\overline{\varphi\_m}(x)dx
\]
如果我们再看第二个复变函数形式的表达式，就有
\[
    c\_m=\frac{1}{2\pi}\int\_{-\pi}^{\pi} f(x)e^{-imx}dx
\]
若进行验证，得到的结果也确实如此.(提示：将$e^{inx}$展开为三角函数，再在$[-\pi,\pi]$积分.)

### 内积运算的法则

下列内积运算的法则会在接下来用到，事实上，若内积能满足下列几个条件，就称为欧基里德空间：

- $(a+c,b)=(a,b)+(c,b)$

- $(a,b+c)=(a,b)+(a,c)$

- $(ka,b)=k(a,b)$

- $(a,kb)=k(a,b)$

- $(a,b)=(b,a)$

## Dirichlet核

### 定义式

Dirichlet核的定义是这样的：
\[
    D_N(x)=\sum\_{-N}^N e^{inx} = \frac{\sin(N+\frac{1}{2})x}{\sin\frac{x}{2}}
\]

第二个等号既可以直接合并$e^{inx}$和$e^{-inx}$得到$\cos nx$的式子从而进行积化和差，又可以利用等比数列的性质得到.

### 搭建起Dirichlet核和原函数的桥梁
针对文章开头提到的第二种定义，可以定义函数数列
\[
    s\_N(x)=\sum\_{-N}^N c\_ne^{inx}
\]
将$c\_n$展开，有
\begin{equation}
    \begin{aligned}
        s\_N(x)&=\sum\_{-N}^N\left(\frac{1}{2\pi}\int_{-\pi}^{\pi} f(t)e^{-int}dt\right)e^{inx}\\\\\\
        &=\int\_{-\pi}^{\pi} \frac{1}{2\pi}f(t)\sum\_{-N}^Ne^{in(x-t)}dt\\\\\\
        &=\frac{1}{2\pi}\int\_{-\pi}^{\pi} f(t)D\_N(x-t)dt\\\\\\
        &=\frac{1}{2\pi}\int\_{-\pi}^{\pi} f(x-t)D\_N(t)dt
    \end{aligned}
\end{equation}
最后一个等号通过函数的周期性和简单的换元运算得到. 至此，Dirichlet核和原函数的桥梁就被搭建起来了. 接下来，需要证明，以这个函数核构建的函数收敛于$f$.

### Bessel不等式以及其重要推论

> 设$f(x)$在正交函数系$\{\varphi\_n(x)\}$下的系数为$\{c\_n\}$, 则有$\sum\_{n=1}^{\infty}|c_n|^2\leq(f,f)$.

设$s\_n(x)=\sum_{m=1}^n c\_m\varphi\_m(x)$, 其中$c\_m=\int_a^b f(x)\overline{\varphi\_m}(x)dx$. 下面通过讨论$s\_n(x)$到$f(x)$的误差得到这个不等式和一个重要的推论.

注意到$(f,s\_n)=\int_a^b f(x)\sum\overline{c\_m}\overline{\varphi\_m(x)}dx=\sum\overline{c\_m}\int_a^b f(x)\overline{\varphi\_m(x)}dx=\sum|c\_m^2|$

以及$(s\_n,s\_n)=\sum|c\_m^2|$
\begin{equation}
    \begin{aligned}
        (f-s\_n,f-s\_n)&=(f,f-s\_n)-(s\_n,f-s\_n)\\\\\\
        &=(f,f)-(f,s\_n)-(s\_n,f)+(s\_n,s\_n)\\\\\\
        &=(f,f)-(s\_n,s\_n)\\\\\\
        &\geq 0
    \end{aligned}
\end{equation}
也就是说，
\[
    (s\_n,s\_n)=\sum\_1^n|c_m|^2\leq(f,f)
\]
$n\to\infty$时，就是所谓的Bessel不等式. 也可以发现，函数的Fourier系数$c\_m$满足$\lim\limits\_{n\to\infty}c\_m=0$. 这个推论会在下面Dirichlet核收敛的证明中用到. 

### 收敛证明
> 若对一些$x$有常数$\delta>0$和$M<\infty$使得\[|f(x+t)-f(x)|\leq M|t|\]对所有$t\in(-\delta,\delta)$成立，那么有\[\lim\limits\_{n\to\infty}s_N(x)=f(x)\]

_要注意的是，我们在这里只讨论逐点收敛._

定义函数
\[
    g(t)=\begin{cases}
    \frac{f(x-t)-f(t)}{\sin(t/2)},0<|t|<\pi\\\\\\
    0,t=0
    \end{cases}
\]
考虑到
\[
    \frac{1}{2\pi}\int\_{-\pi}^{\pi}D_N(x)dx=1
\]
因此有
\[
    \frac{1}{2\pi}\int\_{-\pi}^{\pi}D\_N(t)f(x)dt=f(x)
\]
所求函数和原函数做差，就有
\begin{equation}
    \begin{aligned}
    s_N(x)-f(x)&=\frac{1}{2\pi}\int\_{-\pi}^{\pi}g(t)\sin\left(N+\frac{1}{2}\right)tdt\\\\\\
    &=\frac{1}{2\pi}\int\_{-\pi}^{\pi}\left[g(t)\cos\frac{t}{2}\right]\sin Ntdt+\frac{1}{2\pi}\int\_{-\pi}^{\pi}\left[g(t)\sin\frac{t}{2}\right]\cos Ntdt
    \end{aligned}
\end{equation}
根据$f(x)$的条件和$g(x)$的定义，$g(x)\cos(t/2)$和$g(x)\sin(t/2)$是有界的. 利用Bessel不等式的推论可以发现，这两个积分趋近于$0$. 这就证明了结论.

## 总结&我接下来想写的

写到这里，已经涉及到了很多数学中的基本技巧：三角函数、向量内积、复变函数、等比数列、函数项数列收敛等等. Fourier级数可以说是相当“优美”的一类级数. 在一些领域中，展开式中每一项均具有物理意义，这是其他级数难以企及的. 我们又可以看到，Fourier级数还可以跳出三角函数的限制，放在普遍的无穷维空间的规范正交基. 此外，它的收敛定理相比幂级数而言也是很宽松的. 

接下来还有很多内容，我暂时的打算是这样的：

- Jordan's criterion(关于$s_N(x)$收敛什么时候收敛到什么值)，涉及到“有界差分”的概念.

- Parseval等式和应用（Fourier分析理论的核心内容之一），如三角函数系的完备性

- Fejer核、Poisson核

- Gibbs现象

- ...
