---
layout: post
title: 真正理解拉格朗日乘子法和 KKT 条件
categories: [机器学习]
description: KKT 条件是解决最优化问题的时用到的一种方法。最优化问题通常是指对于给定的某一函数，求其在指定作用域上的全局最小值。
keywords: 机器学习, 拉格朗日乘子法, KKT 条件
tags: [机器学习, KKT, 拉格朗日乘子法]
repost: ["https://www.cnblogs.com/xinchen1111/p/8804858.html", "https://www.cnblogs.com/xinchen1111/p/8804858.html"]
readMins: 30
excerpt: "KKT 条件是解决最优化问题的时用到的一种方法。最优化问题通常是指对于给定的某一函数，求其在指定作用域上的全局最小值。"
---

　　这篇博文以直观的方式讲解了拉格朗日乘子法和 KKT 条件，对偶问题等内容。

### 无约束优化

　　首先从无约束的优化问题讲起，一般就是要使一个表达式取到最小值：

$$
    min\ f(x)
$$

　　如果求 $$max\ f(x)$$ 也可以通过取反转化为求 $$min\ (−f(x))$$ 的问题，然后对它的每一个变量求求，然后让偏导为零，解方程组就行了。

   [![kkt][img1]][img1]{:data-lightbox="kkt"}

　　如图可知，在极值点处一定满足 $$\frac{df(x)}{dx}=0$$（只是必要条件，比如 $$f(x)=x^3$$ 在 $$x=0$$ 处就不是极值点）然后对它进行求解，再代入验证是否真的是极值点就行了，对于有些问题可以直接通过这种方法求出解析解（如最小二乘法）。

　　但是也有很多问题解不出来或者很难解，所以就需要梯度下降法、牛顿法、坐标下降法之类的数值迭代算法了（感知机 、logistic 回归中用到）。

　　对于这些迭代算法就像下面这张图一样，我们希望找到其中的最小值，一个比较直观的想法是先找一个起点，然后不断向最低点靠近，就像把一个小球放到一个碗里一样。

   [![iter][img2]][img2]{:data-lightbox="kkt"}

　　一开始要找一个起始点，然后确定走的方向和距离，最后还要知道什么时候停止，这三步中最难的是确定走的方向，因为走的慢点还可以接受，要是方向错了就找不到最小值了，所以走的距离可以简单的设为一个比较小的值，起始点可以随机选一个 $$(x_0,y_0)$$，然后是确定方向，一般选择 $$(x_0,y_0)$$ 处梯度的反方向，这是函数在这个点下降最快的方向（原因可以看[知乎][href1]中忆臻的回答），它是一个向量，然后它的大小就是走的距离，为了防止太大而走过头，导致不断在最小值附近来回震荡，所以需要乘上一个比较小的因子（称为学习率），最终的停止条件就是梯度的大小很接近于 0（在极值点处的梯度大小为 0），这种方法依靠梯度确定下降方向的方法叫做梯度下降法。

　　对 $$f(x)$$ 求极小值的流程就是：

1. 随机选定 $$x_0$$
1. 得到函数在 $$x_0$$ 的梯度，然后从 $$x_0$$ 向前走一步：$$x_0^{new0}=x_0^{old0}−\alpha\nabla{f(x)}$$
1. 重复第 2 步，直到梯度接近于 0（小于一个事先设定的很小的数），或者到达指定的迭代上限，如下图所示

   [![gradient-des][img3]][img3]{:data-lightbox="kkt"}

    除了这种方法之外，其中第 2 步还可以这样做，将 $$x$$ 固定为常数，这样就变成只有一个变量的优化问题了，直接求导为 0 就可以得到最优点，向前走到 $$(x_0,y_1)$$ 处，然后固定 $$y_1$$, 对 $$x$$ 进行相同的操作，这种每次只优化一个变量的方法叫做坐标下降法，如下图所示

   [![coordlinate-des][img4]][img4]{:data-lightbox="kkt"}

### 等式束优化

    进一步的，我们可能要在满足一定约束条件的情况下最小化目标函数，比如有一个等式约束：

$$
\begin{cases}
    min\ f(x)\\
    s.t.\ h(x) = 0
\end{cases}
$$

   [![extremum-constraint][img5]][img5]{:data-lightbox="kkt"}

    该问题不能通过求 $$f(x)$$ 的极值点来解决，因为这个问题的解可能根本不是 $$min\ f(x)$$ 的解，那么还是要从问题本身去找线索：

    如图，其中的圆圈是指目标函数 $$f(x，y)$$ 投影在平面上的等值线，表示在同一个圆圈上，黑线是约束条件 $$h(x)=0$$ 的函数图像，可知，等值线与函数图像相交的点其实就是所有满足约束的点，那么极值点只有可能在等值线与函数图像相切的地方取到，因为如果在相交的地方取到，那么沿着 $$h(x)$$ 的图像往前走或者往后走，一定还有其它的等值线与它相交，也就是 $$f(x,y)$$ 的值还能变大和变小，所以交点不是极值点，只有相切的时候才有可能是极值点。在相切的地方 $$h(x)$$ 的梯度和 $$f(x,y)$$ 的梯度应该是在同一条直线上的。（这一点可以这么想，在切点处两个函数的梯度都与切平面垂直，所以在一条直线上）

    所以满足条件的极值点一定满足：$$∇f(x,y)=λ∇h(x,y)$$ ( $$λ=0$$ 是允许的，表示 $$f(x,y)$$ 本身的极值点刚好在切点上)，然后和原来的等式方程 $$h(x,y)=0$$ 联立，然后只要解出这个方程组，就可以得到问题的解析解了。当然也存在解不出来的情况，就需要用罚函数法之类的方法求数值解。

    为了方便和好记，就把原来的优化问题写成 $$f(x,y)+λh(x,y)$$ 的形式，然后分别对 $$λ,x,y$$ 求偏导，并令之等于 0，该方法称之为拉格朗日乘数法。

    如果有多个等式约束怎么办呢，如下图：

   [![extremum-multi-constraint][img6]][img6]{:data-lightbox="kkt"}

    这里的平面和球面分别代表了两个约束 $$h_1(x)$$ 和 $$h_2(x)$$，那么这个问题的可行域就是它们相交的那个圆。这里蓝色箭头表示平面的梯度，黑色箭头表示球面的梯度，那么相交的圆的梯度就是它们的线性组合（只是直观上的），所以在极值点的地方目标函数的梯度和约束的梯度的线性组合在一条直线上。所以就满足：

$$
\begin{cases}
   \nabla f(x) = \lambda \sum_{i=1}^{2}{\mu_{i}\nabla h_i(x)}=\sum_{i=1}^{2}\lambda_{i}\nabla h_i(x)\\
h_1(x)=0\\
h_2(x)=0
\end{cases}
$$

    对于大于 2 个约束的情况也一样，令 $$L(x,λ)=f(x)+\sum_{i=1}^{n}λ_i∇h_i(x)$$ 然后分别对 $$x、λ$$ 求偏导并令它们为 0，这个可以看做是一种简记，或者是对偶问题，这个函数叫做拉格朗日函数。

### 不等式约束优化
    再进一步，如果问题中既有等式约束，又有不等式约束怎么办呢？对于：

$$
   \begin{cases}
   min\ f(x)\\
   s.t.\\ 
   \quad h(x) = 0\\
   \quad g(x) \le 0
   \end{cases}
$$

   当然也同样约定不等式是 $$\le$$，如果是 $$\ge$$ 只要取反就行了。对于这个问题先不看等式约束，对于不等式约束和目标函数如下图：

   [![inequation-constraint][img7]][img7]{:data-lightbox="kkt"}

    阴影部分就是可行域，也就是说可行域从原来的一条线变成了一块区域。那么能取到极值点的地方可能有两种情况：

1. 还是在 $$h(x)$$ 和 等值线相切的地方
1. $$f(x)$$ 的极值点本身就在可行域里面

    因为如果不是相切，那么同样的，对任意一个在可行域中的点，如果在它附近往里走或者往外走，$$f(x)$$ 一般都会变大或者变小，所以绝大部分点都不会是极值点，除非这个点刚好在交界处，且和等值线相切，或者这个点在可行域内部，其本身就是 $$f(x)$$ 的极值点，如下图：

   [![inequation-extremum][img8]][img8]{:data-lightbox="kkt"}

    对于右边的情况，不等式约束就变成等式约束了，对 $$f(x)+λh(x)+μg(x)$$ 用拉格朗日乘子法：

$$
   \begin{cases}
      \nabla f(x)+\lambda \nabla h(x)+\mu \nabla g(x) = 0\\
      h(x)=0\\
      g(x)=0\\
      \mu \geq 0
   \end{cases}
$$

    这里需要解释一下，为什么不是 $$μ \ne 0$$ 而是 $$\mu \ge 0$$，后面的约束比前面的更强，已知问题中的可行域是在 $$g(x)≤0$$ 一侧，而由上上个图可知 $$g(x)$$ 的梯度是指向大于 0 的一侧，也就为可行域相反的一侧，而求的问题是极小值，而 $$f(x)$$ 在交点处的梯度是指向可行域的一侧，也就是说两个梯度一定是相反的，所以也就可以确定这里的系数一定是大于 0 的，而等式约束由于不知道 $$h(x)$$ 的梯度方向，所以对它没有约束， 而 $$\mu = 0 $$ 是因为极值点可能刚好在 $$g(x)$$ 上。

    对于左边的情况，不等式约束就相当于没有，对 $$f(x)+\lambda h(x)$$ 用拉格朗日乘子法：

$$
   \begin{cases}
      \nabla f(x)+\lambda \nabla h(x)= 0\\
      h(x)=0\\
      g(x) \leq 0
   \end{cases}
$$

    最好把两种情况用同一组方程表示出来。对比一下两个问题，不同的是第一种情况中有 $$\mu \ge 0$$ 且 $$g(x)=0$$, 第二种情况 $$\mu = 0$$ 且 $$g(x) \le 0$$ ，综合两种情况，可以写成 $$\mu g(x)=0$$ 且 $$\mu \ge 0，g(x) \le 0$$：

$$
   \begin{cases}
      \nabla f(x)+\lambda \nabla h(x)+\mu \nabla g(x) = 0\\
         \mu g(x) = 0\\
         \mu \geq 0 \\
         h(x)=0\\
         g(x) \leq 0
   \end{cases}
$$

### KKT 条件
    上述不等式约束优化就是 KKT 条件，它的含义是这个优化问题的极值点一定满足这组方程组（不是极值点也可能会满足，但是不会存在某个极值点不满足的情况）它也是原来的优化问题取得极值的必要条件，解出来了极值点之后还是要代入验证的。但是因为约束比较多，情况比较复杂，KKT 条件并不是对于任何情况都是满足的。要满足 KKT 条件需要有一些规范性条件（Regularity conditions），就是要求约束条件的质量不能太差，常见的比如：

1. LCQ：如果 $$h(x)$$ 和 $$g(x)$$ 都是形如 $$Ax+b$$ 的仿射函数，那么极值一定满足 KKT 条件。
1. LICQ：起作用的 $$g(x)$$ 函数（$$g(x)$$ 相当于等式约束的情况）和 $$h(x)$$ 函数在极值点处的梯度线性无关，那么极值一定满足 KKT 条件。
1. Slater：如果优化问题是个凸优化问题，且至少存在一个点满足 $$h(x)=0$$ 和 $$g(x)=0$$，极值一定满足 KKT 条件，并且满足强对偶性质。

    这里的 Slater 条件比较重要，因为它可以推导出强对偶性质（比 KKT 条件还好）。它需要原问题是凸优化问题，所谓凸优化就是这个优化问题的优化函数是凸函数，并且可行域是凸集，可行域数凸集就要求其中的 $$h(x) \le 0$$ 的条件中 $$h(x)$$ 必须也是凸函数，而 $$g(x) \le 0$$ 中的 $$g(x)$$ 必须是 $$Ax+b$$ 形式的，也就是仿射函数（比如二维的情况，可行域就在 $$g(x)$$ 这条曲线上，那么 $$g(x)$$ 必须得是直线才能满足凸集的定义）。

    其它条件还有很多，可以看[维基百科][href2]。

    如果有多组等式约束 $$h_i(x)=0(i=1,..,n)$$, 和不等式约束 $$g_i(x) \ne 0(i=1,..,n)$$ 也是一样，只要做个线性组合就行了：

$$
   \begin{cases}
      \nabla f(x)+\sum_{i=1}^{n}\lambda_i \nabla h_i(x)+\sum_{i=1}^{n}\mu_i \nabla g_i(x) = 0\\
      \mu_i g(x)_i = 0\\
      \mu_i \geq 0\\
      h_i(x)=0\\
      g_i(x) \leq 0\\
      i = 1,2,...,n
   \end{cases}
$$

    问题到这里就大致解决了，KKT 条件虽然从理论上给出了极值的必要条件，但是一般实际解的时候直接方程也是很困难的（特别是约束很多的时候），一般也会采用罚函数法等数值方法。

### 对偶问题
    为了更好的解决这个优化问题，数学家还找到了它的对偶问题，找一个优化问题的对偶问题的一般因为是对偶问题比原问题更好解决，并且对偶问题的解和原问题是一样的，上面的拉格朗日函数也可以看做原问题的对偶问题。

    为了去掉问题中的约束，可以把它们作为惩罚项加到目标函数中 $$min_xf(x)+Mh(x)+Ng(x)$$ 其中 M, N 是两个很大的正数，在数值解法中可以直接这样做，这个就是罚函数法的思路。不过在理论推导时这样做是不严谨的，除非 M, N 为无穷大，可改写 $$L(x,μ,λ)=min_{x}max_{\mu,\lambda} f(x)+\lambda h(x)+\mu g(x)$$。这个式子可以这么理解，现在外层给定任意一个 $$x_0$$ 值，然后内层在给定的 $$x_0$$ 下优化那个函数，让它最小。然后外层选能够让内层得到的值最大的一个 $$x_0$$，得到的函数表达式就是：

$$
   L(x,\mu,\lambda)=
            \left\{\begin{matrix}
            f(x) & (x \quad满足约束)\\
            \infty & (x \quad不满足约束)\\ 
            \end{matrix}\right.
$$

    所以外层选的那个 $$x_0$$ 一定满足约束，否则，内层的 $$max$$ 的时候会让 $$\mu$$ 或者 $$\lambda$$ 为无穷大，外层不会选那些能让内层得到无穷大的 $$x$$ 值，这样改写就和原来的带约束形式完全一致了，但是形式不同。这样可以利用 $$max[min\ f(x)] \le min[max\ f(x)]$$ 这个公式（这个很好理解，$$min\ f(x) \le min[max\ f(x)]$$, 然后就有这个公式了），得到原问题的最小值的一个下界，就是:

$$
   min_{x}max_{\mu,\lambda}f(x) + \lambda h(x) + \mu g(x)  \geq  max_{\mu,\lambda}min_{x}f(x) + \lambda h(x) + \mu g(x)
$$

    前面的就是原函数，后面的是它的一个下界。那么为什么要这样做呢? 是因为后面的一定是一个凸规划（理论上证明了的），比较好解决。但是这个只是一个下界，它们之间还是有一定的差距。这个差距叫对偶误差（duality gap）。对偶误差如果为 0 其实是一个非常好的性质，表示可以直接求解后面的问题得到原问题的解，这种性质叫强对偶性质，否则就只是弱对偶。

    强对偶性质非常好，但是要求也很苛刻，比 KKT 条件要苛刻。如果问题满足强对偶一定也满足 KKT 条件，反之不一定。对于这类优化问题，KKT 条件、强对偶、规范性条件之间的关系是：

   [![kkt-rc-relation][img9]][img9]{:data-lightbox="kkt"}


[href1]: https://www.zhihu.com/question/36301367
[href2]: https://en.wikipedia.org/wiki/Karush%E2%80%93Kuhn%E2%80%93Tucker_conditions

[img1]: /images/post/ml/extremum-value-sketch.png
[img2]: /images/post/ml/extremum-iter.jpg
[img3]: /images/post/ml/gradient-des.jpg
[img4]: /images/post/ml/coordlinate-des.jpg
[img5]: /images/post/ml/extremum-constraint.png
[img6]: /images/post/ml/extremum-multi-constraint.png
[img7]: /images/post/ml/kkt-inequation-constraint.png
[img8]: /images/post/ml/kkt-extremum-inequation.png
[img9]: /images/post/ml/kkt-rc-relation.png
