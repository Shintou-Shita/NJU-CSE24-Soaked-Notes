# Ch.2 随机变量及其概率分布



### 随机变量

定义：设 $\varOmega=\{e\}$ 是随即试验的样本空间，如果对每个 $e\in\varOmega$，都对应一个单值实函数 $X=X(e)$，则称 $X$ 为随机变量.

概率分布：随机变量 $X$ 取值的概率称为 $X$ 的概率分布.

随机变量的**分布函数**：设 $X$ 为一个随即变量，$x$ 是任何实数，称函数

$$
F(x)=\mathrm{Pr}(X\le x),-\infty<x<+\infty
$$

为随机变量 $X$ 的分布函数.

**分布函数的性质**：

(1) $F(x)$ 单调不减，即 $\forall x_1<x_2$ 有 $F(x_1)\le F(x_2)$.

(2) $0\le F(x)\le 1$ 且 $F(-\infty)=\lim_{x\to-\infty}F(x)=0,F(+\infty)=\lim_{x\to +\infty}F(x)=1$.

(3) $F(x)$ 右连续，即 $F(x_0+0)=\lim_{x\to x_0^+}F(x)=F(x_0)$.

任一随机变量的分布函数必然满足以上三条性质，满足以上三条性质的任一函数必然是某随机变量的分布函数.

### 离散型随机变量及其分布

**离散型随机变量**：若随机变量 $X$ 的可能取值为有限个或可列无限多个，则称其为离散型随机变量.

**离散型随机变量的分布律**：设离散型随机变量 $X$ 的所有可能取值为 $x_1,x_2,\cdots,x_n,\cdots$，$X$ 取值 $x_k$ 的相应概率为 p_k，即：

$$
\mathrm{Pr}(X=x_k)=p_k,k=1,2,\cdots
$$

称其为离散型随机变量 $X$ 的分布律，或以表格形式给出：

```python
X | x_1 | x_2 | ... | x_n | ...
--+-----+-----+-----+-----+-----
P | p_1 | p_2 | ... | p_n | ...
```

**分布律的性质**：

(1) $p_k\ge 0,k=1,2,\cdots$.

(2) $\sum_{k}p_k=1$.

常用离散型随机变量分布：

- 0-1 分布、两点分布、Bernoulli 分布
  
    离散型随机变量 $X$ 服从参数为 $p$ 的 0-1 分布，记为 $X\sim B(1,p)$.
    
    分布律：
    
    $$
    \text{Pr}(X=1)=p, \text{Pr}(X=0)=q
    $$
    
    其中：$0<p<1, q = 1 - p$ 
    
    期望与方差：
    
    $$
    \text{E}(X)=p,\text{Var}(X)=pq
    $$
    
- 二项分布
  
    离散型随机变量 $X$ 服从参数为 $n,p$ 的二项分布，记为 $X\sim B(n,p)$.
    
    分布律：
    
    $$
    \text{Pr}(X=k)=\binom{n}{k}p^kq^{n-k},k=0,1,\cdots,n
    $$
    
    其中：$0<p<1,q=1-p$ 
    
    期望与方差：
    
    $$
    \text{E}(X)=np,\text{Var}(X)=npq
    $$
    
- 泊松分布、Poisson 分布
  
    离散型随机变量 $X$ 服从参数为 $\lambda$ 的二项分布，记为 $X\sim P(\lambda)$.
    
    分布律：
    
    $$
    \text{Pr}(X=k)=\dfrac{\lambda^k}{k!}\mathrm{e}^{-\lambda}
    $$
    
    其中 $\lambda>0$ 为常数.
    
    期望与方差：
    
    $$
    \text{E}(X)=\lambda,\text{Var}(X)=\lambda
    $$
    
    泊松分布常用于描述大量时间中稀有事件出现频数的概率模型.
    
- 几何分布
  
    离散型随机变量 $X$ 服从参数为 $p$ 的二项分布，记为 $X\sim G(p)$.
    
    分布律：
    
    $$
    \text{Pr}(X=k)=q^{k-1}p,k=1,2,3,\cdots
    $$
    
    其中：$0<p<1$ 是常数，$q=1-p$.
    
    期望与方差：
    
    $$
    \text{E}(X)=\dfrac{1}{p},\text{Var}(X)=\dfrac{q}{p^2}
    $$
    
    几何分布的无记忆性：$\text{Pr}(X=s+t|X>t)=\text{Pr}(X=s)$
    

### 连续性随机变量及其分布

**连续型随机变量**：其取值不能一一列举. 设随机变量 $X$ 的分布函数为 $F(x)$，若存在非负可积函数 $p(x)$，对任意实数 $x$ 有：

$$
F(x)=\int_{-\infty}^{x}p(t)\mathrm{d}t
$$

则称 $X$ 为连续型随机变量，称函数 $p(x)$ 为 $X$ 的**概率密度函数**，简称**密度函数**.

**密度函数的性质**：

(1) $p(x)\ge 0$.

(2) $\int_{-\infty}^{+\infty}p(x)\mathrm{d}x=1$.

(3) $\forall a<b, P(a<X\le b)=F(b)-F(a)=\int_{a}^{b}p(x)\mathrm{d}x$.

(4) 因 $p(x)$ 可积，根据微积分性质，$F(x)$ 连续.

(5) 若 $p(x)$ 在点 $x$ 处连续，则 $F(x)$ 在 $x$ 处可导，且 $p(x)=F’(x)$.

常用连续型随机变量分布：

- 均匀分布
  
    连续型随机变量 $X$ 在区间 $[a,b]$ 上服从均匀分布，即 $X\sim U[a,b]$，则其概率密度函数和分布函数如下：
    
    $$
    p(x)=\begin{cases}
    \dfrac{1}{b-a},&a<x<b,\\
    0,&\text{otherwise}.
    \end{cases},
    F(x)=\begin{cases}
    0,&x<a,\\
    \dfrac{x-a}{b-a},&a\le x<b,\\
    1,&x\ge b.
    \end{cases}
    $$
    
    期望和方差如下：
    
    $$
    \mathrm{E}X=\dfrac{a+b}{2},\mathrm{Var}X=\dfrac{1}{12}(b-a)^2
    $$
    
- 指数分布
  
    对于常数 $\lambda>0$，连续型随机变量 $X$ 服从参数为 $\lambda$ 的指数分布，即 $X\sim E(\lambda)$，则其概率密度函数和分布函数如下：
    
    $$
    p(x)=\begin{cases}
    \lambda \mathrm{e}^{-\lambda x},&x\ge 0,\\
    0, &x<0.
    \end{cases},
    F(x)=\begin{cases}
    1-\mathrm{e}^{-\lambda x},&x\ge 0,\\
    0,&x<0.
    \end{cases}
    $$
    
    期望和方差如下：
    
    $$
    \mathrm{E}X=\lambda,\mathrm{Var}X=\lambda^2
    $$
    
    该分布常用于描述各种寿命的分布.
    
- 正态分布
  
    对于常数 $\mu$ 和正常数 $\sigma>0$，连续型随机变量 X 服从参数为 $\mu,\sigma^2$ 的正态分布，即 $X\sim N(\mu,\sigma^2)$，则其概率密度函数如下：
    
    $$
    p(x)=\dfrac{1}{\sqrt{2\pi}\sigma}\mathrm{exp}\left(-\dfrac{(x-\mu)^2}{2\sigma^2}\right)
    $$
    
    期望和方差如下：
    
    $$
    \mathrm{E}X=\mu,\mathrm{Var}X=\sigma^2
    $$
    
    性质：
    
    (1) 曲线 $p(x)$ 关于 $x=\mu$ 对称，且 $\forall b>0$ 有 $\mathrm{Pr}(X\le \mu-b)=\mathrm{Pr}(X\ge \mu +b)$.
    
    (2) $x\to\pm\infty$ 时 $p(x)\to 0$，即曲线以 $x$ 轴为渐近线.
    
    (3) $x=\mu$ 时 $p(x)$ 取到最大值 $\dfrac{1}{\sqrt{2\pi}\sigma}$，又因密度图形覆盖面积总为 $1$，故固定 $\mu$ 时，$\sigma$ 越小，最大值越大，图形越高越陡峭；$\sigma$ 越大，最大值越小，图形越低越平缓.
    
    (4) 固定 $\sigma$，而 $\mu$ 变化时，曲线横向平移.
    
    (5) 当 $\mu=0,\sigma=1$ 时，$X\sim N(0,1)$，称此时其服从标准正态分布，其密度函数和分布函数特别记为 $\varphi(x)$ 与 $\varPhi(x)$. 其显然有 $\varPhi(-x)=1-\varPhi(x)$.
    
    (6) 若 $X\sim N(\mu,\sigma^2)$，则 $Z=\dfrac{X-\mu}{\sigma}\sim N(0,1)$，故而欲计算服从某正态分布的连续型随机变量在某区间的概率，常常将其标准化配合 $\varPhi(x)$ 的图表进行近似计算.
    
    (7) $3\sigma$ 法则：(6) 的特例，$2\varPhi(1)-1\approx 0.6826, 2\varPhi(2)-1\approx 0.9544, 2\varPhi(3)-1\approx 0.9974$.
    

### 随机变量函数的分布

(1) 离散型随机变量的函数，枚举即可. 

设 $X$ 为离散型随机变量，其分布律为 $\mathrm{Pr}(X=x_k)=p_k,k=1,2,\cdots$，对于 $X$ 的函数 $Y=g(X)$，其分布律为：

$$
\mathrm{Pr}(Y=y_k)=\sum_{i,y_k=g(x_i)}p_i
$$

(2) 连续型随机变量的函数，求解常采用分布函数法.

设 $X$ 为连续型随机变量，$y=g(x)$ 为连续实函数，则 $Y=g(X)$ 也是连续型随机变量，先求解 Y 的分布函数 $F_Y(y)$：

$$
F_Y(y)=\mathrm{Pr}(Y\le y)=\mathrm{Pr}(g(X)\le y)=\int_{x:g(x)\le y}p_X(x)\mathrm{d}x
$$

然后 $p_Y(y)=F’_Y(y)$.

(3) 特别地，设随机变量 $X$ 的可能取值范围为 $(a,b)$，$X$ 的概率密度为 $p_X(x), a<x<b$（$a,b$ 不必有限），设函数 $y=g(x)$ 处处可导，且 $g’(x)$ 恒正（或恒负），则 $Y=g(X)$ 为连续型随机变量，其概率密度为：

$$
p_Y(y)=\begin{cases}
p_X(g^{-1}(y))\cdot |(g^{-1}(y))'|,&\alpha<y<\beta,\\
0,&\text{otherwise.}
\end{cases}
$$

其中 $\alpha=\min\{g(a),g(b)\},\beta=\max\{g(a),g(b)\},g^{-1}(y)$ 为 $y=g(x)$ 的反函数.