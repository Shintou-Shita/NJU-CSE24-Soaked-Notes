# Ch.6 统计量与抽样分布

### 总体与样本

**定义**：在数理统计中我们将所研究的对象的全体称为总体，将总体中每个成员称为个体.

**样本**：为了对总体 $X$ 进行研究，通常要从总体中随机地抽取一些个体，这些个体就称为样本，抽得样本的过程称为抽样，样本中个体的数量称为样本容量.

设对总体进行了 $n$ 次观测，得到一组数据 $(x_1, x_2, \cdots, x_n)$，称其为样本观察值或样本值.

**样本的二重性**：我们通常将样本看成一组数，通常用小写字母表示，记为 $(x_1, x_2, \cdots, x_n)$ 而在考虑一般问题时，我们谈到样本，往往将其看做一组随机变量，通常用大写字母表示，记为 $(X_1, X_2, \cdots, X_n)$.

研究这一组随机变量，就要研究其分布，为了使样本能够反映总体的特征，我们对随机抽样作出如下两点要求：

(1) 代表性：样本的每个分量 $X_i$ 与总体 $X$ 有相同的分布.

(2) 独立性：$X_1, X_2, \cdots, X_n$ 相互独立.

**简单随机样本**：满足上述两点性质的样本称为简单随机样本，也通常简称为样本.

**分布函数**：设总体 X 的分布函数为 $F(x)$，则样本 $(X_1, X_2, \cdots, X_n)$ 的分布函数为：

$$
F(x_1,x_2,\cdots, x_n)=\prod_{i=1}^{n}F(x_i)
$$

**概率密度函数**：若总体是连续型随机变量，其概率密度函数为 $p(x)$，则样本 $(X_1, X_2, \cdots, X_n)$ 的概率密度函数为：

$$
p(x_1,x_2,\cdots,x_n)=\prod_{i=1}^{n}p(x_i)
$$

### 统计量与抽样分布

**统计量**：设 $(X_1, X_2, \cdots, X_n)$ 为总体 $X$ 的一个样本，$T(x_1, x_2, \cdots, x_n)$ 为不含任何未知参数的函数，则称 $T(X_1, X_2, \cdots, X_n)$ 为一个统计量.

统计量是样本的函数，但因统计量中不含任何未知量，故一旦有了样本，就可以计算出统计量. 下面介绍一些常用的统计量：

设 $(X_1, X_2, \cdots, X_n)$ 为总体 $X$ 中抽取的一个样本，下述统计量称为**样本均值**：

$$
\bar{X}=\dfrac{1}{n}\sum_{i=1}^{n}X_i
$$

下述统计量称为**样本方差**：

$$
S^2=\dfrac{1}{n-1}\sum_{i=1}^{n}(X_i-\bar{X})^2
$$

- 这里的分母为什么是 $n-1$？
  
    这是为了保证**无偏性**.
    
    **自由度**的解释：我们已经用到了 $\bar{X}$，故而确定了 $n-1$ 个变量，便确定了 $n$ 个变量，故而除以自由度 $n-1$.
    
    更详细的**无偏性**的解释：无偏估计（unbiased estimator）是指在已知样本时，这个无偏估计必须是所有估计中的平均值，换句话说，我们应当保证 $\mathrm{E}(S^2)=\sigma^2$，其中 $\sigma^2$ 为总体方差（population variance），这样 $S^2$ 就被称作是无偏估计的。
    
    接下来我们进行推导，设总体均值为 $\mu$，总体方差为 $\sigma^2$，样本平均为 $\bar{x}$，样本容量为 $n$，于是：
    
    $$
    \begin{aligned}
    \hat\sigma^2
    &:=\dfrac{1}{n}\sum_{i=1}^{n}(x_i-\bar{x})^2 \\
    &=\dfrac{1}{n}\sum_{i=1}^{n}(x_i-\mu)^2+\dfrac{2}{n}\sum_{i=1}^{n}(x_i-\mu)(\mu-\bar{x})+\dfrac{1}{n}\sum_{i=1}^{n}(\mu-\bar{x})^2\\
    &=S^2-\dfrac{2}{n}\sum_{i=1}^{n}(\mu^2-(\bar{x}+x_i)\mu+x_i\bar{x})+n\times \dfrac{1}{n}(\mu-\bar{x})^2\\
    &=S^2-2\mu^2+4\mu\bar{x}-2\bar{x}^2+(\mu-\bar{x})^2\\
    &=S^2-(\bar{x}-\mu)^2
    \end{aligned}
    $$
    
    两边取期望得到：
    
    $$
    \begin{aligned}
    \mathrm{E}\left(\dfrac{1}{n}\sum_{i=1}^{n}(x_i-\bar{x})^2\right)
    &=\mathrm{E}(S^2-(\bar{x}-\mu)^2)\\
    &=\mathrm{E}(S^2)-\mathrm{E}((\bar{x}-\mu)^2)\\
    &\xlongequal{\text{unbiased}}\sigma^2-\mathrm{E}((\bar{x}-\mu)^2)
    \end{aligned}
    $$
    
    因 $\mathrm{E}((\bar{x}-\mu)^2)$ 是针对所有取样本时 $(\bar{x}-\mu)^2$ 取值的均值，根据 CLT（中心极限定理），我们有 $\bar{x}\sim N\left(\mu, \dfrac{\sigma^2}{n}\right)$，注意！各 $x_i$ 独立，且单独一个的方差为 $\sigma^2$ ，可以使用 CLT. 于是就直接导出了：
    
    $$
    \mathrm{E}((\bar{x}-\mu)^2)=\mathrm{Var}(\bar{x})=\dfrac{\sigma^2}{n}
    $$
    
    最终得到：
    
    $$
    \mathrm{E}(\hat{\sigma}^2)
    =\dfrac{n-1}{n}\sigma^2\Leftrightarrow \mathrm{E}\left(\dfrac{n}{n-1}\hat{\sigma}^2\right)
    =\sigma^2
    $$
    
    也就是
    
    $$
    S^2=\dfrac{n}{n-1}\hat{\sigma}^2=\dfrac{1}{n-1}\sum_{i=1}^{n}(x_i-\bar{x})^2
    $$
    
    即得. 不难发现这个式子成立和无偏要求可互推.
    

与之对比，我们称下述统计量为**样本二阶中心矩**：

$$
S^{*2}=\dfrac{1}{n}\sum_{i=1}^{n}(X_i-\bar{X})^2
$$

下述统计量为**样本标准差**：

$$
S=\sqrt{\dfrac{1}{n-1}\sum_{i=1}^{n}(X_i-\bar{X})^2}
$$

下述统计量为**样本 $k$ 阶原点矩**：

$$
A_k=\dfrac{1}{n}\sum_{i=1}^{n}{X_i}^k,k=1,2,3,\cdots
$$

下述统计量为**样本 $k$ 阶中心矩**：

$$
B_k=\dfrac{1}{n}\sum_{i=1}^{n}(X_i-\bar{X})^k,k=1,2,3,\cdots
$$

**样本相关系数**：

$$
r=\dfrac{S_{XY}}{S_X^*\cdot S_Y^*}\\
S_{XY}=\dfrac{1}{n}\sum_{i=1}^{n}(X_i-\bar{X})(Y_i-\bar{Y})
$$

因样本具有二重性，故而统计量作为样本的函数同样具有二重性，即在一次具体的观察中，统计量是具体的数值；脱离具体的观察或试验，统计量应堪称随机变量. 统计量的分布称为**抽样分布**. 研究统计量的分布对于统计推断十分重要，一般来说，要确定一个统计量的精确分布十分困难，只有在**正态总体**的情况下，有比较好的结论. 对于一般情形，我们通常利用概率论中的极限定理求出统计量的极限分布，这种方法称为大样本理论.

### 正态总体

正态总体是实际总体的一个较好的近似，我们线介绍一下三大分布：

**$\chi^2$ 分布**

定义：设 $X_1, X_2,\cdots, X_n$ 为独立同分布的随机变量且均服从标准正态分布 $N(0,1)$，则称随机变量

$$
\chi_n^2:=\sum_{i=1}^{n}X_i^2
$$

为服从自由度为 $n$ 的 $\chi^2$ 分布，记为 $\chi_n^2\sim \chi^2(n)$.

$\chi^2$ 分布由现代统计学的奠基人之一 Pearson 提出，其密度函数如下：

$$
p(x)=\begin{cases}
\dfrac{\mathrm{e}^{-\frac{x}{2}}x^{\frac{n}{2}-1}}{2^{n/2}\Gamma(n/2)}, &x>0,\\
0, &x\le 0.
\end{cases}
$$

- Gamma 函数补漏
  
    定义式：
    
    $$
    \Gamma(z)=\int_{0}^{\infty}\mathrm{e}^{-t}t^{z-1}\mathrm{d}t,\operatorname{Re}z>0
    $$
    
    一些性质：
    
    1. $\Gamma(1)=1$. proof. 代入简单计算即可.
    2. $\Gamma(z+1)=z\Gamma(z)$. proof. 定义+分部积分.
    3. $\Gamma(n+1)=n!, n\in\mathbb{N}$. proof. 相同递推关系，归纳即可.
    4. $\Gamma(\frac{1}{2})=\sqrt{\pi}$. proof. 换元并使用著名的高斯积分 $\int_{-\infty}^{+\infty}\mathrm{e}^{-x^2}\mathrm{d}x=\sqrt{\pi}$.
    5. Digamma 函数：定义：
    
    $$
    \psi(z):=\dfrac{\mathrm{d}(\ln\Gamma(z))}{\mathrm{d}z}=\dfrac{\Gamma'(z)}{\Gamma(z)}
    $$
    
    特殊值：
    
    $$
    \psi(n)=H_{n-1}-\gamma,n\in\mathbb{Z}_+
    $$
    
      | $\psi(1)=-\gamma$                                            | $\psi'(1)=\dfrac{\pi^2}{6}$                                  |
      | ------------------------------------------------------------ | ------------------------------------------------------------ |
      | $\psi(1/2)=-\gamma-2\ln 2$                                   | $\psi'(1/2)=\dfrac{\pi^2}{2}$                                |
      | $\psi(-1/2)=-\gamma-2\ln 2+2$                                | $\psi'(-1/2)=\dfrac{\pi^2}{2}+4$                             |
      | $\psi(1/4)=-\gamma-\dfrac{\pi}{2}-3\ln 2$                    | $\psi(3/4)-\gamma+\dfrac{\pi}{2}-3\ln 2$                     |
      | $\psi(1/3)=-\gamma-\dfrac{\pi}{2\sqrt{3}}-\dfrac{3}{2}\ln 3$ | $\psi(2/3)=-\gamma+\dfrac{\pi}{2\sqrt{3}}-\dfrac{3}{2}\ln 3$ |
    
       递推公式：
    
    $$
        \psi(z+n)=\psi(z)+\sum_{k=0}^{n-1}\dfrac{1}{z+k},n\in\mathbb{N}
    $$
    
       余元公式：
    
    $$
        \psi(1-z)-\psi(z)=\pi\cot(\pi z)
    $$
    
       积分表示：
    
    $$
        \psi(z)=\int_{0}^{\infty}\left(\dfrac{\mathrm{e}^{-t}}{t}-\dfrac{\mathrm{e}^{-zt}}{1-\mathrm{e}^{-t}}\right)\mathrm{d}t,\operatorname{Re}z>0
    $$
    
       Polygamma 函数：
    
    $$
        \psi^{(n)}(z)=\dfrac{\mathrm{d}^n}{\mathrm{d}z^n}\psi(z)
    $$
    
       $n=1$ 时称为 Trigamma 函数.
    
    $$
        \psi^{(m)}(z+n)-\psi^{(m)}(z)=(-1)^{m}m!\sum_{k=0}^{n-1}\dfrac{1}{(k+z)^{m+1}}\\
        \psi^{(n)}(1)=\begin{cases}
        -\gamma,&n=0,\\
        (-1)^{n+1}n!\zeta(n+1),&n\in\mathbb{Z}_+.
        \end{cases}
    $$
    
    6. Beta 函数/B 函数/第一欧拉积分
      
        定义：
    
    $$
        B(p,q)=\int_{0}^{1}t^{p-1}(1-t)^{q-1}\mathrm{d}t,\operatorname{Re}p>0,\operatorname{Re}q>0
    $$
    
       等式：
    
    $$
        \begin{aligned}
        B(p,q)&=B(q,p)\\
        B(p,q)&=\dfrac{\Gamma(p)\Gamma(q)}{\Gamma(p+q)}\\
        B(z,1-z)&=\dfrac{\pi}{\sin(\pi z)}
        \end{aligned}
    $$
    
       无穷乘积表示
    
       Euler 无穷乘积表示
    
    $$
        \Gamma(z)=\prod_{k=1}^{\infty}\left(\dfrac{k}{z+k-1}\right)\left(\dfrac{k+1}{k}\right)^{z-1}
    $$
    
       Weierstrass 无穷乘积表示
        
    $$
    \Gamma(z)=\dfrac{1}{z\mathrm{e}^{z\gamma}}\prod_{k=1}^{\infty}\dfrac{k}{z+k}\mathrm{e}^{z/k}
    $$
    

性质：

1. 若 $\chi_1^2\sim \chi^2(n_1),\chi_2^2\sim \chi^2(n_2)$，且二者相互独立，则$\chi_1^2+\chi_2^2\sim\chi^2(n_1+n_2)$.
2. 若$\chi^2\sim \chi^2(n)$，则 $\mathrm{E}\chi^2=n,\mathrm{Var}\chi^2=2n$.
3. Cochran 分解定理/柯赫伦分解定理
   
    设 $X_1,X_2,\cdots, X_n$ 为独立同分布的随机变量，均服从 $N(0,1)$，又设秩为 $n_i$ 的 $X_1, X_2,\cdots, X_n$ 的非负二次型 $Q_i, i=1,2,\cdots, k$ 满足：
    
    $$
    Q_1+Q_2+\cdots+Q_k=\sum_{i=1}^{n}X_i^2
    $$
    
    则 $Q_i$ 相互独立且分别服从自由度为 $n_i$ 的 $\chi^2$ 分布的充要条件为：
    
    $$
    n_1+n_2+\cdots+n_k=n
    $$
    
    这个定理有矩阵版本.
    

**t 分布**

设 $X\sim N(0,1), Y\sim \chi^2(n)$，且 $X$ 与 $Y$ 相互独立，则称随机变量

$$
T=\dfrac{X}{\sqrt{Y/n}}
$$

服从自由度为 $n$ 的 $t$ 分布，记作 $T\sim t(n)$.

t 分布由英国统计学家 W. Gosset 以笔名 Student 发表，故而又称为学生分布（Student 分布），其密度函数如下：

$$
p(x)=\dfrac{\Gamma\left(\frac{n+1}{2}\right)}{\sqrt{n\pi}\Gamma\left(\frac{n}{2}\right)}\left(1+\dfrac{x^2}{n}\right)^{-\frac{n+1}{2}}
$$

显然该函数为偶函数，可以证明当 $n\to\infty$ 时 $p(x)\to \varphi(x)$，换句话说 $n$ 足够大时 t 分布可近似为 $N(0,1)$.

**F 分布**

设 $U\sim \chi^2(n_1),V\sim \chi^2(n_2)$，且 $U,V$ 相互独立，则称随机变量：

$$
F=\dfrac{U/n_1}{V/n_2}
$$

服从自由度为 $(n_1,n_2)$ 的 $F$ 分布，记作 $F\sim F(n_1, n_2)$.

F 分布由现代统计学的奠基人之一 Fisher 提出，其密度函数如下：

$$
p(x)=\dfrac{\Gamma((n_1+n_2)/2)}{\Gamma(n_1/2)\Gamma(n_2/2)}\left(\dfrac{n_1}{n_2}\right)^{\frac{n_1}{2}}x^{\frac{n_1}{2}-1}\left(1+\dfrac{n_1}{n_2}x\right)^{-\frac{n_1+n_2}{2}},x>0
$$

另 $x\le 0$ 时 $p(x)=0$. 

一些性质如下：

1. 若 $F\sim F(n_1, n_2)$，则 $\dfrac{1}{F}\sim F(n_2,n_1)$.
2. 若 $T\sim t(n)$，则 $T^2\sim F(1, n)$.

**上 $\alpha$ 分位点**

定义：设 X 是一个随机变量，对于一个给定的数 $\alpha(0<\alpha <1)$，成满足下述条件的实数 $\lambda_\alpha$ 为 $X$ 的上 $\alpha$ 分位点.

$$
\mathrm{Pr}(X>\lambda_\alpha)=\alpha
$$

记法：

当 $X$ 服从 $N(0,1), \chi^2(n),t(n),F(n_1,n_2)$ 时，上 $\alpha$ 分位点 $\lambda_\alpha$ 分别记为：$u_\alpha, \chi_\alpha^2(n),t_\alpha(n),F_\alpha(n_1,n_2)$.

一些性质：

1. $u_{1-\alpha}=-u_\alpha, t_{1-\alpha}=-t_\alpha(n)$.
2. $F_{1-\alpha}(n_1,n_2)=\dfrac{1}{F_\alpha(n_2,n_1)}$.

**正态总体的样本与样本方差的分布**

对于正态总体，样本均值与样本方差及其相关的某些统计量的分布具有非常完美的结论，这些结论对于参数估计与假设检验具有重要的意义，结果由下述定理给出：

**定理**：设 $X_1, X_2,\cdots, X_n$ 是来自正态总体 $N(\mu,\sigma^2)$ （即独立同分布为该分布）的一个样本，则：

(1) $\bar{X}\sim N(\mu, \dfrac{\sigma^2}{n})$.

(2) $(n-1)S^2/\sigma^2\sim \chi^2(n-1)$.

(3) $\bar{X}$ 与 $S^2$ 相互独立.

**推论 1**：设 $X_1, X_2,\cdots, X_n$ 是来自正态总体 $N(\mu,\sigma^2)$ 的一个样本，则：

$$
T:=\dfrac{\sqrt{n}(\bar{X}-\mu)}{S}\sim t(n-1)
$$

**推论 2**：设 $X_1, X_2,\cdots, X_{n_1}$ 是来自正态总体 $N(\mu_1,\sigma_1^2)$ 的一个样本，设 $Y_1, Y_2,\cdots, Y_{n_2}$ 是来自正态总体 $N(\mu_2,\sigma_2^2)$ 的一个样本，且两样本相互独立，记 $\bar{X}$ 和 $\bar{Y}$ 分别为其样本均值，$S_1^2, S_2^2$ 分别为其样本方差，则：

$$
F:=\dfrac{S_1^2\sigma_2^2}{S_2^2\sigma_1^2}\sim F(n_1-1,n_2-1)
$$

**推论 3**：设 $X_1, X_2,\cdots, X_{n_1}$ 是来自正态总体 $N(\mu_1,\sigma_1^2)$ 的一个样本，设 $Y_1, Y_2,\cdots, Y_{n_2}$ 是来自正态总体 $N(\mu_2,\sigma_2^2)$ 的一个样本，且两样本相互独立，则：

$$
T:=\sqrt{\dfrac{n_1n_2(n_1+n_2-2)}{n_1+n_2}}\dfrac{(\bar{X}-\bar{Y})-(\mu_1-\mu_2)}{\sqrt{(n_1-1)S_1^2+(n_2-1)S_2^2}}\sim t(n_1+n_2-2)
$$

### 多元正态分布理论*

Source: 回归分析|笔记整理（3）——多元正态分布理论（上） - 知乎 - 学弱渣：https://zhuanlan.zhihu.com/p/46665398

前置线性代数内容：

1. 称方阵 $A$ 为幂等阵当且仅当 $A^2=A$，容易证明其特征值为 $0$ 或 $1$.
2. 若 $A_{n\times n}$ 为对称幂等阵，且 $\mathrm{rank}(A)=r$，那么存在正交阵 $P_{n\times n}$，使得 $A=P\begin{bmatrix} I_r &0 \\ 0 &0\\ \end{bmatrix}P^{\mathsf{T}}$. 正交阵即 $PP^{\mathsf{T}}=I$ 的阵.
3. 若 $A$ 对称幂等，则 $\mathrm{tr}(A)=\mathrm{rank}(A)$.
4. 若 $A_{n\times n}$ 对称幂等，且 $\mathrm{rank}(A)=r$，则存在列满秩矩阵 $B_{n\times r}$ 使得 $A=B(B^{\mathsf{T}}B)^{-1}B^{\mathsf{T}}$.
5. 正交投影阵：对任一列满秩矩阵 $A$，定义正交投影阵 $P_A=A(A^{\mathsf{T}}A)^{-1}A^{\mathsf{T}}$，不难发现其必为一个对称幂等阵.
6. $\forall x\in\mathbb{R}^n$，设 $P$ 为 $n$ 阶正交投影阵，那么存在分解式 $x=y+z$ 使得 $y=Pz, z=(I-P)x$，且 $y^{\mathsf{T}}z=0$.

**均值向量**：设 $X=(X_1,X_2\cdots X_p)^{\mathsf{T}}$ 为 $p$ 维随机变量，称下述为 $X$ 的均值向量：

$$
\mathrm{E}X:=(\mathrm{E}X_1,\mathrm{E}X_2,\cdots,\mathrm{E}X_n)^{\mathsf{T}}
$$

**协差**：定义 $\mathrm{Var}X=\mathrm{Cov}X=\mathrm{E}((X-\mathrm{E}X)(X-\mathrm{E}X)^{\mathsf{T}})$ 为随机变量 $X$ 的协差，是一个矩阵，显然：$(\mathrm{Cov}X)[i,j]=\mathrm{Cov}(X_i,X_j)$，并且矩阵是半正定矩阵.

设 $A$ 是常数阵，$X$ 是随机变量，则 $\mathrm{Cov}(AX)=A\mathrm{Cov}(X)A^{\mathsf{T}}$.

**协方差**：设 $X, Y$分别是 $p,q$ 维向量，定义二者的协方差： $\mathrm{Cov}(X,Y)=\mathrm{E}((X-\mathrm{E}X)(Y-\mathrm{E}Y)^{\mathsf{T}})$.

设 $A,B$ 是常数阵，$X,Y$ 是随机变量 $\mathrm{Cov} (AX,BY)=A\mathrm{Cov}(X,Y)B^{\mathsf{T}}$.

**二次型**：设 $X$ 为 $p$ 维列向量，$A$ 为 $p\times p$ 的对称阵，则称 $X^\mathsf{T}AX$ 为 $X$ 的二次型，显然其是关于 $X$ 各分量的二次项之和.

二次型的均值：设 $\mathrm{E}X=\mu,\mathrm{Cov}X=\Sigma$，则 $\mathrm{E}(X^\mathsf{T}AX)=\mu^\mathsf{T}A\mu+\mathrm{tr}(A\Sigma)$.

**$p$ 元正态分布**：设 $X=(X_1,\cdots, X_n)$ 为 $p$ 维随机变量，若其联合密度函数为：

$$
f(x)=(2\pi)^{-p/2}|\Sigma|^{-1/2}\exp\left(-\frac{1}{2}(x-\mu)^\mathsf{T}\Sigma^{-1}(x-\mu)\right)
$$

其中 $\mu=(\mu_1,\cdots, \mu_n)^{\mathsf{T}}$，$\Sigma_{p\times p}$ 正定，则称 $X$ 服从参数为 $\mu$ 和 $\Sigma$ 的 $p$ 元正态分布，记作 $X\sim N_p(\mu,\Sigma)$，显然其均值向量和协差 为 $\mu$ 和 $\Sigma$.

当 $\mu=\vec{0},\Sigma=I_p$ 时转化为多元标准正态分布，$X$ 各分量为独立同标准正态分布.

**标准化与平方根阵**：

平方根阵：设 $\Sigma=P^{-1}JP$，其中 $J$ 是 $\Sigma$ 的 Jordan 标准型，那么定义其平方根阵为：$\Sigma^{1/2}=P^{-1}J^{1/2}P$.

标准化：$Y=\Sigma^{-1/2}(X-\mu)$.

多元正态分布的更一般定义：设 $X$ 为 $p$ 维随机变量，若存在 $p\times r$ 阶的列满秩矩阵 $A$ 使得 $X=AY+\mu$，其中 $Y\sim N_r(\vec{0},I_r)$，且 $\mu$ 为常数向量，则称 $X\sim N_p(\mu, AA^{\mathsf{T}})$.

### 正态总体相关定理的证明*

**定理**：设 $X_1, X_2,\cdots, X_n$ 是来自正态总体 $N(\mu,\sigma^2)$ （即独立同分布为该分布）的一个样本，则：

(1) $\bar{X}\sim N(\mu, \dfrac{\sigma^2}{n})$.

(2) $(n-1)S^2/\sigma^2\sim \chi^2(n-1)$.

(3) $\bar{X}$ 与 $S^2$ 相互独立.

proof.

(1) 因 $X_1,X_2,\cdots,X_n$ 独立同分布于 $N(\mu,\sigma^2)$，故而 

$$
\bar{X}=\dfrac{1}{n}\sum_{i=1}^{n} X_i\sim N(\dfrac{1}{n}\times n\mu,\dfrac{1}{n^2}\times n\sigma^2)
$$

也就是 $\bar{X}\sim N\left(\mu,\dfrac{\sigma^2}{n}\right)$.

(2)

构造如下矩阵 $A$，并令 $\vec{Y}=A\vec{X}$：

$$
\begin{bmatrix}
\mathbf{u}_1\\
\mathbf{u}_2\\
\vdots\\
\mathbf{u}_n
\end{bmatrix},
\mathbf{u}_1=\dfrac{1}{\sqrt{n}}\mathbf{1}_n,
\mathbf{u}_i=\dfrac{1}{\sqrt{i(i-1)}}(\mathbf{1}_{i-1},-i+1,\mathbf{0}_{n-i})(i\ne 1)
$$

这个矩阵是这样构造的，首先 $\mathbf{u}_1$ 的构造是因为这使得 $Y_1=\mathbf{u}_1\vec{X}=\sqrt{n}\bar{X}$，然后使用施密特正交化的方式构造 $\mathbf{u}_i$.

首先因 $A$ 的正交性，故：

$$
\vec{Y}^\mathsf{T}\vec{Y}=\vec{X}^\mathsf{T}A^\mathsf{T}A\vec{X}=\vec{X}^\mathsf{T}\vec{X}
$$

也就是 $\sum_{i=1}^{n} X_i^2=\sum_{i=1}^{n}Y_i^2$.

根据 $\vec{Y}=A\vec{X}$ 不难得到 $Y_1\sim N\left(\sqrt{n}\mu,\sigma^2\right),Y_i\sim N(0,\sigma^2),i\ne 1$.

同时因 $(X_1,\cdots,X_n)\sim N(\mu\vec{1}_n,\sigma^2 I_n)$，故 $(Y_1,\cdots, Y_n)\sim N(\mu A\vec{1}_n,A(\sigma^2I_n)A^\mathsf{T})=N((\sqrt{n}\mu,\mathbf{0}_{n-1})^\mathsf{T},\sigma^2 I_n)$。

注：这个结论直接根据正态分布的线性性得到，推广可以得到如下结论：

设 $X\sim N_p(\mu, \Sigma)$，$B$ 为任意的 $m\times p$ 的常数阵，$Y=BX$，随即有：

$$
Y\sim N_m(B\mu,B\Sigma B^\mathsf{T})
$$

由协差阵说明 $\vec{Y}$各分量独立，然后：

$$
\begin{aligned}
\dfrac{(n-1)S^2}{\sigma^2}
&=\dfrac{1}{\sigma^2}\sum_{i=1}^{n}(X_i-\bar{X})^2\\
&=\dfrac{1}{\sigma^2}\left(\sum_{i=1}^{n}X_i^2-n\bar{X}^2\right)\\
&=\dfrac{1}{\sigma^2}\left(\sum_{i=1}^{n}Y_i^2-Y_1^2\right)\\
&=\sum_{i=2}^{n}\left(\dfrac{Y_i}{\sigma}\right)^2\\
&\sim\chi^2(n-1)
\end{aligned}
$$

Q.E.D.

(3) 由 (2) 得知：$\bar{X}=\dfrac{1}{\sqrt{n}}Y_1,S^2=\dfrac{1}{n-1}\sum_{i=2}^{n}Y_i^2$，而 $Y$ 各分量独立，自然有 $\bar{X}$ 和 $S^2$ 独立。Q.E.D.