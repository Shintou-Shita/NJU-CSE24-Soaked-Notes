# Ch.4 随机变量的数字特征

### 离散型随机变量的数学期望/期望/均值

定义：设离散型随机变量 X 的分布律为 $\text{Pr}(X=x_i)=p_i,i=1,2,\cdots$，若级数 $\sum_{i=1}^{+\infty} |x_i|p_i$ 收敛，则称 $\sum_{i=1}^{+\infty} x_ip_i$ 为 $X$ 的数学期望（expected value），记为 $\text{E}X$ 或 $EX$，即

$$
\text{E}X=\sum_{i=1}^{+\infty} x_ip_i
$$

**数学期望不存在**：若 $\sum_{i=1}^{+\infty} |x_i|p_i$ 发散，则称 $X$ 的数学期望不存在.

要求级数绝对收敛的原因： $\sum_{i=1}^{+\infty} x_ip_i$ 必须不因 $x_i$ 次序的变化而改变，故而仅要求条件收敛是不够的，必须要求其绝对收敛。

### 连续型随机变量的数学期望/期望/均值

定义：设连续型随机变量 $X$ 的密度函数为 $p(x)$，若积分 $\int_{-\infty}^{+\infty} |x|p(x)\mathrm{d}x <+\infty$，则称 $\int_{-\infty}^{+\infty} xp(x)\mathrm{d}x$ 为 $X$ 的数学期望或均值，记为 $\text{E}X$ 或 $EX$，即

$$
\text{E}X=\int_{-\infty}^{+\infty} xp(x)\mathrm{d}x
$$

期望不存在的例子：连续型柯西（Cauchy）分布 $p(x)=\dfrac{1}{\pi(1+x^2)},x\in(-\infty,+\infty)$.

**随机变量的函数**：设随机变量 $X$ 的函数 $Y=g(X)$ 也是一个随机变量，则有：

(1) 若 $X$ 为离散型随机变量，其分布律为 $\text{Pr}(X=x_k)=p_k,k=1,2,\cdots$，若 $\sum_{k=1}^{+\infty}|g(x_k)|p_k$ 收敛，则

$$
\text{E}Y=\sum_{k=1}^{+\infty}g(x_k)p_k
$$

(2) 若 $X$ 为连续型随机变量，其密度函数为 p(x)，若 $\int_{-\infty}^{+\infty}|g(x)|p(x)\mathrm{d}x<+\infty$，则

$$
\text{E}Y=\int_{-\infty}^{+\infty}g(x)p(x)\mathrm{d}x 
$$

该定理可以被推广到随机向量情形：设随机向量 $(X,Y)$ 的函数 $Z=g(X,Y)$ 是一个随机变量，则：

(1) 若 $(X,Y)$ 为离散型随机向量，其联合分布律为 $\text{Pr}(X=x_i,Y=y_j)=p_{i,j},i,j=1,2,\cdots$，若 $\sum_{i=1}^{+\infty}\sum_{j=1}^{+\infty}|g(x_i,y_j)|p_{i,j}$ 收敛，则

$$
\text{E}Z=\sum_{i=1}^{+\infty}\sum_{j=1}^{+\infty}g(x_i,y_j)p_{i,j}
$$

(2) 若 $(X,Y)$ 为连续型随机向量，其联合密度为 $p(x,y)$，若：$\int_{-\infty}^{+\infty}\int_{-\infty}^{+\infty} |g(x,y)|p(x,y)\mathrm{d}x\mathrm{d}y<+\infty$，则

$$
\text{E}Z=\int_{-\infty}^{+\infty}\int_{-\infty}^{+\infty} g(x,y)p(x,y)\mathrm{d}x\mathrm{d}y
$$

**期望的性质**：

1. 设 $a$ 为常数，则 $\text{E}(a)=a$.
2. 线性性：对任意有限常数 $a,b$，我们有 $\text{E}(aX+bY)=a\text{E}X+b\text{E}Y$.
3. 若 $X,Y$ 相互独立，则 $\text{E}(XY)=\text{E}X\cdot\text{E}Y$.

### 方差与均方差/标准差

定义：设 $X$ 是一个随机变量，若 $\text{E}(X^2)<+\infty$，则称 $\text{E}(X-\text{E}X)^2$ 为随机变量 $X$ 的方差（variance），记为 $\text{D}X$ 或 $\text{Var}(X)$，同时称 $\sqrt{\text{Var}(X)}$ 为 $X$ 的均方差或标准差，记为 $\sigma(X)$.

计算公式：

(1) 若 $X$ 为离散型随机变量，其分布律为 $\text{Pr}(X=x_k)=p_k,k=1,2,\cdots$，则

$$
\text{Var}(X)=\sum_{k=1}^{+\infty}(x_k-\text{E}X)^2\text{Pr}(X=x_k)
$$

(2) 若 $X$ 为连续型随机变量，其密度函数为 $p(x)$，则

$$
\text{Var}(X)=\int_{-\infty}^{+\infty} (x-\text{E}X)^2p(x)\mathrm{d}x
$$

(3) 此外根据期望的线性性，有计算公式：

$$
\text{Var}(X)=\text{E}(X^2)-\text{E}^2(X)
$$

**方差的性质**：

(1) 对于任意常数 $a$，有 $\text{Var}(a)=0$.

(2) 设 $a,b$ 为任意有限常数，若 $X$ 的方差存在，则 $\text{Var}(aX+b)=a^2\text{Var}(X)$.

(3) 对任意存在方差的随机变量 $X, Y$，有：

$$
\text{Var}(X\pm Y)=\text{Var}(X)+ \text{Var}(Y)\pm 2\text{E}((X-\text{E}X)(Y-\text{E}Y))
$$

### 切比雪夫不等式（Chebyshev’s inequality）

定理：设随机变量 $X$ 的期望 $\text{E}X$ 和方差 $\text{Var}(X)$ 均存在，则对于任意的 $\varepsilon>0$，有：

$$
\text{Pr}(|X-\text{E}X|\ge \varepsilon)\le\dfrac{\text{Var}(X)}{\varepsilon^2} 
$$

推论：若 $\text{Var}X=0$，则 $X\equiv \text{E}X$，即 $X$ 是一个常数.

### 协方差与相关系数

协方差：对随机变量 $X$ 和 $Y$，若 $\text{E}X$ 和 $\text{E}Y$ 和 $\text{E}(XY)$ 均存在，则称 $\text{E}((X-\text{E}X)(Y-\text{E}Y))$ 为 $X$ 和 $Y$ 的协方差（covariance），记为 $\text{Cov}(X,Y)$，即

$$
\text{Cov}(X,Y)=\text{E}((X-\text{E}X)(Y-\text{E}Y))
$$

其可以看作是方差的推广：$\text{Var}(X)=\text{Cov}(X,X)$.

计算公式：

$$
\text{Cov}(X,Y)=\text{E}(XY)-\text{E}X\cdot \text{E}Y
$$

**协方差的性质**：

(1) 对称性：$\text{Cov}(X,Y)=\text{Cov}(Y,X)$.

(2) 对常数 $a,b,c,d\in\mathbb{R}$，有 $\text{Cov}(aX+c,bY+d)=ab\text{Cov}(X,Y)$.

(3) $\text{Cov}(X_1+X_2,Y)=\text{Cov}(X_1,Y)+\text{Cov}(X_2,Y)$.

(4) 若 $X$ 和 $Y$ 独立，$\text{Cov}(X,Y)=0$.

注：(4) 可由期望性质：独立变量之积之期望为变量期望之积和协方差计算公式立得.

**柯西-施瓦茨不等式（Cauchy-Schwarz inequality）在概率论中的形式**

设随机变量 $X$ 和 $Y$ 的方差均存在，则：

$$
\text{Cov}^2(X,Y)\le \text{Var}(X)\cdot \text{Var}(Y)
$$

等号成立当且仅当存在不全为零的常数 $a$ 和 $b$ 使得 $\text{Pr}(Y=aX+b)=1$.

- proof
    
    proof.
    
    对任意的 $t\in\mathbb{R}$，定义函数：
    
    $$
    u(t)=\text{E}(t(X-\text{E}X)-(Y-\text{E}Y))^2
    $$
    
    由期望线性性知：
    
    $$
    u(t)=t^2\text{Var}(X)-2t\text{Cov}(X,Y)+\text{Var}(Y)
    $$
    
    显然 $u(t)\ge 0$，由判别式知：
    
    $$
    \text{Cov}^2(X,Y)\le \text{Var}(X)\cdot \text{Var}(Y)
    $$
    
    等号成立的条件是 $u(t)=0$ 有一个二重实根，设为 $t_0$，随即有：
    
    $$
    \text{Var}(t_0(X-\text{E}X)-(Y-\text{E}Y))={t_0}^{2}\text{Var}(X)-2t_0\text{Cov}(X,Y)+\text{Var}(Y)=u(t_0)=0
    $$
    
    随即根据方差的计算公式得知：$\text{E}(t_0(X-\text{E}X)-(Y-\text{E}Y))=0$.
    
    根据方差的性质：$\text{Pr}(t_0(X-\text{E}X)-(Y-\text{E}Y)=0)=1$.
    

**标准化随机变量**：已知随机变量 $X$ 的均值 $\text{E}X$ 和方差 $\text{Var}(X)$，做如下变换：

$$
X^*=\dfrac{X-\text{E}X}{\sqrt{\text{Var}(X)}}
$$

则 $\text{E}X^*=0, \text{Var}(X^*)=1$. 称 $X^*$ 为 $X$ 的标准化随机变量.

**相关系数**：设随机变量 X 和 Y 的方差均存在，且 $\text{Var}(X),\text{Var}(Y)>0$，则称

$$
\text{Corr}(X,Y)=\rho_{XY}=\dfrac{\text{Cov}(X,Y)}{\sqrt{\text{Var}(X)\text{Var}(Y)}}
$$

为 $X$ 和 $Y$ 的相关系数.

正相关/负相关：若 $\text{Corr}(X,Y)>0$，则称 $X$ 和 $Y$ 正相关，若 $\text{Corr}(X,Y)<0$，则称 $X$ 和 $Y$ 负相关.

**相关系数的性质**：

(1) $\text{Corr}(X,Y)=\text{Cov}(X^*,Y^*)$

(2) $|\text{Corr}(X,Y)|\le 1$. 等号成立的充要条件是存在不同时为零的常函数 $a,b$ 使得 $\text{Pr}(Y=aX+b)=1$，即 $X$ 和 $Y$ 以概率 $1$ 有线性关系.

(3) 线性无关/不相关：随机变量 $X$ 和 $Y$ 的相关系数 $\text{Corr}(X,Y)=0$. 若随机变量 $X$ 和 $Y$ 独立，则 $X$ 和 $Y$ 不相关，反之未必成立.

**不相关的等价条件**：以下四个命题相互等价：

(1) $\text{Corr}(X,Y)=0$.

(2) $\text{Cov}(X,Y)=0$.

(3) $\text{E}(XY)=\text{E}(X)\text{E}(Y)$.

(4) $\text{Var}(X\pm Y)=\text{Var}(X)\pm \text{Var}(Y)$. 

相关系数刻画了随机变量之间的线性相关特征，但不相关只说明没有线性关系，不代表没有非线性函数关系，故而一般独立性与不相关不等价. 但正态分布时，独立性与不相关等价，即下述事实：

设 $(X,Y)\sim N(\mu_1,\mu_2,\sigma_1^2,.\sigma^2)$，则其独立性和不相关性等价. 只因 $\text{Corr}(X,Y)=\rho$，而 $\rho=0$ 时 $X,Y$ 独立，同时 $X,Y$ 独立很容易就能根据不相关的等价条件得知其不相关.

### 矩与协方差阵

设 X 是一个随机变量，对正整数 k，若 $\text{E}(|X|^k)<\infty$，则称 $\text{E}(X^k)$ 为 $X$ 的 $k$ 阶原点矩 或 $k$ 阶矩；若 $\text{E}(|X-\text{E}X|^k)<\infty$，则 $\text{E}((X-\text{E}X)^k)$ 为 $X$ 的 $k$ 阶中心矩.

**偏度**：随机变量标准化后的三阶矩.

**峰度**：随机变量标准化后的四阶矩.

对于 $n$ 维随机向量 $X=(X_1,X_2,\cdots, X_n)^{\mathsf{T}}$，定义其数学期望及协方差阵：

$$
\text{E}X=(\text{E}X_1,\text{E}X_2,\cdots,\text{E}X_n)^{\mathsf{T}}
$$

称为 $X$ 的数学期望.

$$
\varSigma=(\text{Cov}(X_i,X_j))_{n\times n}=
\begin{bmatrix}
\text{Cov}(X_1,X_1)&\text{Cov}(X_1,X_2)&\cdots&\text{Cov}(X_1,X_n)\\
\text{Cov}(X_2,X_1)&\text{Cov}(X_2,X_2)&\cdots&\text{Cov}(X_2,X_n)\\
\vdots&\vdots&\ddots&\vdots\\
\text{Cov}(X_n,X_1)&\text{Cov}(X_n,X_2)&\cdots&\text{Cov}(X_n,X_n)\\
\end{bmatrix}
$$

称为 $X$ 的协方差阵，其显然是一个对称阵.