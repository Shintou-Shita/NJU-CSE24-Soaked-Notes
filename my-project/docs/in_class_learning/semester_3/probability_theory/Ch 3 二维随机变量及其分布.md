# Ch.3 二维随机变量及其分布



### 二维随机变量

**二维随机变量的联合分布函数/分布函数**：设 $(X,Y)$ 为二维随机变量，对任意实数 $(x,y)$，二元函数

$$
F(x,y)=\text{Pr}((X\le x)\cap(Y\le y))=\text{Pr}(X\le x,Y\le y)
$$

称为二维随机变量 (X,Y) 的联合分布函数，简称分布函数.

**性质**：

(1) $F(x,y)$ 分别是 $x$ 和 $y$ 的单调不减函数，即 $x_2>x_1\rightarrow F(x_2,y)\ge F(x_1,y)\land y_2>y_1\rightarrow F(x,y_2)\ge F(x_1,y)$ 为真.

(2) 必有 $0\le F(x,y)\le 1$，且 $F(-\infty, y)=F(x,-\infty)=F(-\infty, -\infty)=0, F(+\infty, +\infty) =1$.

(3) $F(x,y)$ 关于 $x,y$ 右连续，即 $F(x+0,y)=F(x,y+0)=F(x,y)$.

(4) 对任意实数 $x_2>x_1, y_2>y_1$，有 $1\ge F(x_2,y_2)-F(x_2, y_1)-F(x_1,y_2)+F(x_1,y_1)\ge 0$.

当 $F$ 为分布函数时，上述四条成立；反之若某函数满足上述四条，则必然存在随机变量使之成为其分布函数.

**边缘分布与边缘分布函数**

定义：对于二维随机变量 $(X,Y)$，单个随机变量 $X$ 或 $Y$ 的分布称为边缘分布,

已知二维随机变量 $(X,Y)$ 的联合分布函数 $F(x,y)$，可以轻易得到其边缘分布函数：

$$
F_X(x)=F(x,+\infty),F_Y(y)=F(+\infty,y)
$$

**推广**：$n$ 维随机变量的边缘分布函数：

已知 $n$ 维随机变量 $(X_1,X_2,\cdots,X_n)$ 的联合分布函数 $F(x_1,x_2,\cdots,x_n)$，可以轻易得到其 $k$ 维边缘分布函数：

$$
F_{(X_{i_1},\cdots,X_{i_k})}(\cdots,+\infty,x_{i_1},+\infty,\cdots,x_{i_k})=F(c_1,\cdots,c_n)\\
c_{i_{j}}=x_{i_{j}},c_t=+\infty(\text{otherwise})
$$

**独立性条件**：设随机变量 $X,Y$ 满足，对任意 $x,y$，随机事件 $X\le x$ 与 $Y\le y$ 独立，即

$$
\text{Pr}(X\le x,Y\le y)=\text{Pr}(X\le x)\text{Pr}(Y\le y)
$$

即

$$
F(x,y)=F_X(x)F_Y(y)
$$

则称随机变量 $X, Y$ 相互独立.

**性质**：

若随机变量 $X,Y$ 相互独立，$f(x), g(y)$ 为 $X,Y$ 的连续或分段连续函数，则随机变量的函数 $f(X)$ 与 $g(Y)$ 相互独立.

### 二维离散型随机变量

**定义**：若二维随机变量 $(X,Y)$ 的可能取值时有限多个或可列无限多个，则称 $(X,Y)$ 为离散型随机变量.

**联合分布律**：设二维离散型随机变量 $(X,Y)$ 的所有可能取值为 $(x_i,y_j),i,j=1,2,\cdots$ 则：

$$
\text{Pr}(X=x_i,Y=y_j)=p_{i,j}
$$

或其二维表格形式，称为 $(X,Y)$ 的联合分布律.

**性质**：

(1) $p_{i,j}\ge 0$.

(2) $\sum_{i=1}^{\infty}\sum_{j=1}^{\infty}p_{i,j}=1$.

**边缘分布**：

$$
\text{Pr}(X=x_i)=\sum_{j=1}^{\infty}\text{Pr}(X=x_i,Y=y_j)=\sum_{j=1}^{\infty}p_{i,j}=:p_{i,\bullet}
$$

或其表格形式，称为 $X$ 的（边缘）分布律.

同理有：$p_{\bullet, j}=\sum_{i=1}^{\infty} p_{i,j}$.

**联合分布律和边缘分布率在同一表中的形式**如下：

![QQ_1762258584725.png](QQ_1762258584725.png)

**联合分布函数**：

$$
F(x,y)=\sum_{x_i\le x}\sum_{y_j\le y}p_{i,j}
$$

**边缘分布函数**：

$$
F_X(x)=\sum_{x_i\le x}p_{i,\bullet},F_{Y}(y)=\sum_{y_j\le y}p_{\bullet,j}
$$

**区域取值**：

$$
\text{Pr}((X,Y)\in D)=\sum_{(x_i,y_j)\in D}p_{i,j}
$$

**独立性条件**：

$$
p_{i,j}=p_{i,\bullet}\cdot p_{\bullet,j}
$$

**常用二维离散型随机变量分布**

三项分布：$(X,Y)\sim T(n,p_1,p_2)$

其中：$0<p_1,p_2,p_1+p_2<1$.

分布律：

$$
\text{Pr}(X=i,Y=j)=\dfrac{n!}{i!j!(n-i-j)!}{p_1}^{i}{p_2}^j(1-p_1-p_2)^{n-i-j}\\
i,j=0,1,\cdots,n,i+j\le n
$$

边缘分布：是二项分布，即 $X\sim B(n,p_1), Y\sim B(n,p_2)$.

**三项分布是二项分布的推广，是多项分布的一种**.

二维超几何分布

分布律：

$$
\text{Pr}(X=n_1,Y=n_2)=\dfrac{\binom{N_1}{n_1}\binom{N_2}{n_2}\binom{N_3}{n_3}}{\binom{N}{n}}
$$

其中 $N=N_1+N_2+N_3,n=n_1+n_2+n_3$.

### 二维连续型随机变量

定义：对于二维随机变量 $(X,Y)$ 的分布函数 $F(x,y)$，若存在非负函数 $p(x,y)$，使得对于任意的 $(x,y)$，有：

$$
F(x,y)=\int_{-\infty}^x\int_{-\infty}^y p(u,v)\mathrm{d}u\mathrm{d}v
$$

则称 $(X,Y)$ 是二维连续型随机变量，称 $p(x,y)$ 是 $(X,Y)$ 的联合概率密度函数，简称概率密度.

**性质**：

(1) $p(x,y)\ge 0$.

(2) $\int_{-\infty}^{+\infty}\int_{-\infty}^{+\infty} p(u,v)\mathrm{d}u\mathrm{d}v=F(+\infty,+\infty)=1$.

(3) 设 $D$ 是平面区域，则随机点 $(X,Y)$ 落入 $D$ 内的概率为：

$$
\text{Pr}((X,Y)\in D)=\iint_{D}p(x,y)\mathrm{d}x\mathrm{d}y
$$

(4) 若 $p(x,y)$ 在点 $(x,y)$ 处连续，则：

$$
\dfrac{\partial^2F(x,y)}{\partial x\partial y}=p(x,y)
$$

**边缘分布函数与边缘密度函数**：

**边缘分布函数**：

$$
F_X(x)=F(x,+\infty)=\int_{-\infty}^x\int_{-\infty}^{+\infty}p(t,y)\mathrm{d}y\mathrm{d}t\\
F_Y(y)=F(+\infty,y)=\int_{-\infty}^{y}\int_{-\infty}^{+\infty}p(x,t)\mathrm{d}x\mathrm{d}t
$$

**边缘密度函数**：

$$
p_X(x)=F_{X}'(x)=\int_{-\infty}^{+\infty}p(x,y)\mathrm{d}y\\
p_Y(y)=F_Y'(y)=\int_{-\infty}^{+\infty}p(x,y)\mathrm{d}x
$$

**独立性条件**：

用边缘分布函数描述：

$$
F(x,y)=F_X(x)F_Y(y)\qquad\forall (x,y)
$$

或者用边缘密度函数描述：

$$
p(x,y)=p_X(x)p_Y(y)\qquad\forall (x,y)
$$

**上述结果可以推广至 $n$ 维随机变量**：

概率密度：

$$
F(x_1,x_2,\cdots,x_n)=\int_{-\infty}^{x_1}\int_{-\infty}^{x_2}\cdots\int_{-\infty}^{x_n}p(x_1,x_2,\cdots,x_n)\mathrm{d}x_1\mathrm{d}x_2\cdots \mathrm{d}x_n
$$

$k$ 维边缘分布函数：

$$
F_{(X_{i_1},\cdots,X_{i_k})}(\cdots,+\infty,x_{i_1},+\infty,\cdots,x_{i_k})=F(c_1,\cdots,c_n)\\
c_{i_{j}}=x_{i_{j}},c_t=+\infty(\text{otherwise})
$$

独立性条件：$(X_1,X_2,\cdots, X_n)$ 相互独立，当

$$
p(x_1,x_2,\cdots,x_n)=p_{X_1}(x_1)p_{X_2}(x_2)\cdots p_{X_n}(x_n)\qquad \forall (x_1,x_2,\cdots x_n)
$$

**常用二维连续性随机变量分布**

二维均匀分布

设 $D$ 为平面有界区域，其面积为 $S_D$，若二维连续型随机变量 (X,Y) 的联合密度为：

$$
p(x,y)=\begin{cases}
\frac{1}{S_D}, &(x,y)\in D,\\0, &\text{otherwise}.
\end{cases}
$$

则称 $(X,Y)$ 服从区域 $D$ 上的二维均匀分布.

性质：对于 $D_k\subseteq D$：

$$
\text{Pr}((X,Y)\in D_k)=\dfrac{S_{D_k}}{S_D}
$$

二维正态分布：$(X,Y)\sim N(\mu_1,\mu_2,\sigma_1^2,\sigma_2^2,\rho)$

若二维随机变量 $(X,Y)$ 的联合密度为：

$$
p(x,y)=\dfrac{1}{2\pi\sigma_1\sigma_2\sqrt{1-\rho^2}}\mathrm{exp}\left(-\dfrac{\left(\dfrac{x-\mu_1}{\sigma_1}\right)^2-2\rho \left(\dfrac{x-\mu_1}{\sigma_1}\right)\left(\dfrac{y-\mu_2}{\sigma_2}\right)+\left(\dfrac{y-\mu_2}{\sigma_2}\right)^2}{2(1-\rho^2)} \right)
$$

其中 $\mu_1,\mu_2$ 均为常数，$\sigma_1,\sigma_2>0,|\rho|<1$ 均为常数，则称 $(X,Y)$ 符合二维正态分布.

性质：

(1) 边缘分布：$X\sim N(\mu_1,\sigma_1^2), Y\sim N(\mu_2,\sigma_2^2)$.

(2) 独立的充要条件：$\rho=0$.

### 条件分布

设 X 的分布函数为 $F(x)=\text{Pr}(X\le x)$，则随机事件 $A =\{X\in S\}$ 发生条件下的条件分布函数：

$$
F(x|A)=\text{Pr}(X\le x|A)
$$

**离散型随机变量的条件分布**

设 $(X,Y)$ 为二维离散型随机变量，其概率分布律为 $\text{Pr}(X=x_i,Y=y_j)=p_{i,j},i,j=1,2,\cdots$，称

$$
\text{Pr}(X=x_i|Y=y_j)=\dfrac{\text{Pr}(X=x_i,Y=y_j)}{\text{Pr}(Y=y_j)}=\dfrac{p_{i,j}}{p_{\bullet,j}}
$$

为 $Y=y_j$ 条件下，随机变量 $X$ 的条件分布律，表格形式如下：

```
X|_{Y=y_j}    |         x_1           |  \cdots  |         x_i           |  \cdots
--------------+-----------------------+----------+-----------------------+----------
P             | p_{1,j}/p_{\bullet,j} |  \cdots  | p_{i,j}/p_{\bullet,j} |  \cdots 
```

同理，

$$
\text{Pr}(Y=y_j|X=x_i)=\dfrac{\text{Pr}(X=x_i,Y=y_j)}{\text{Pr}(X=x_i)}=\dfrac{p_{i,j}}{p_{i,\bullet}}
$$

为 $X=x_i$ 条件下，随机变量 $Y$ 的条件分布律.

显然，当 $X,Y$ 独立时，条件分布成为无条件分布.

**连续型随机变量的条件分布**

对于二维连续型变量 $(X,Y)$，若下述极限存在，则称为 $Y=y$ 条件下 $X$ 的条件分布函数，记为 $F_{X|Y=y}(x)$.

$$
\lim_{\varepsilon\to 0}\text{Pr}(X\le x|y\le Y<y+\varepsilon)=\lim_{\varepsilon\to 0}\dfrac{\text{Pr}(X\le x,y\le Y<y+\varepsilon)}{\text{Pr}(y\le Y<y+\varepsilon)}\qquad \forall \varepsilon>0
$$

对定义展开得到：

$$
F_{X|Y=y}(x)=\int_{-\infty}^x\dfrac{p(u,y)}{p_Y(y)}\mathrm{d}u
$$

求导得到条件密度函数：

$$
p_{X|Y=y}(x)=\dfrac{p(x,y)}{p_Y(y)}
$$

同理有 $X=x$ 条件下 $Y$ 的条件分布函数与条件密度函数：

$$
F_{Y|X=x}(y)=\int_{-\infty}^{y}\dfrac{p(x,v)}{p_X(x)}\mathrm{d}v,p_{Y|X=x}=\dfrac{p(x,y)}{p_X(x)}
$$

显然，当 $X,Y$ 独立时，条件分布成为无条件分布.

### 二维随机变量函数的分布

**离散型随机变量函数的分布**：

设二维离散型随机变量 (X,Y) 的分布律为 $\mathrm{Pr}(X=x_i,Y=y_j)=p_{i,j},i,j=1,2,\cdots$，若 (X,Y) 的函数 $Z = g(X,Y)$，因其取值集合必然可数，故设其可能取值为 $z_k, k=1,2,\cdots$，其概率分布为：

$$
\mathrm{Pr}(Z=z_k)=\sum_{g(x_i,y_j)=z_k}p_{i,j}
$$

**连续型随机变量函数的分布**

连续型随机变量 $(X,Y)$ 的函数 $Z=g(X,Y)$ 可能是离散型，也可能是连续型.

对于前者，可以枚举其取值得到 $Z$ 的分布律.

对于后者，通常利用分布函数法来求解，即

$$
F_Z(z)=\mathrm{Pr}(g(X,Y)\le Z)=\iint_{D_z}p(x,y)\mathrm{d}x\mathrm{d}y.D_z=\{(x,y)|g(x,y)\le z\}
$$

求出其分布函数后求导得到概率密度 $p_Z(z)$.

以下为集中常用函数的分布公式

**和与差的分布**

通过分布函数法和一些还原操作可以得到，对于 $Z=X+Y$：

$$
p_Z(z)=\int_{-\infty}^{+\infty}p(x,z-x)\mathrm{d}x=\int_{-\infty}^{+\infty}p(z-y,y)\mathrm{d}y\\
$$

特别地，当 $X$ 和 $Y$ 独立时，式子转化为 $p_X$ 和 $p_Y$ 的卷积，故而下述公式亦称为卷积公式：

$$
p_Z(z)=\int_{-\infty}^{+\infty}p_X(x)p_Y(z-x)\mathrm{d}x=\int_{-\infty}^{+\infty}p_X(z-y)p_Y(y)\mathrm{d}y\\
$$

类似地，对于 $Z=X-Y$，有：

$$
p_Z(z)=\int_{-\infty}^{+\infty}p(x,x-z)\mathrm{d}x=\int_{-\infty}^{+\infty}p(z+y,y)\mathrm{d}y\\
$$

**积与商的分布**

对于 $Z=XY$：

$$
p_Z(z)=\int_{-\infty}^{+\infty}p\left(x,\dfrac{z}{x}\right)\dfrac{\mathrm{d}x}{|x|}=\int_{-\infty}^{+\infty}p\left(\dfrac{z}{y},y\right)\dfrac{\mathrm{d}y}{|y|}
$$

对于 $Z=X/Y$：

$$
p_Z(z)=\int_{-\infty}^{+\infty}p(x,zx)|x|\mathrm{d}x=\int_{-\infty}^{+\infty}p(zy,y)|y|\mathrm{d}y
$$

$\max$ **与 $\min$ 的分布**

设随机变量 $X$ 和 $Y$ 相互独立，且 $M=\max(X,Y),N=\min(X,Y)$，则：

$$
F_M(z)=F_X(z)F_Y(z),F_N(z)=1-(1-F_X(z))(1-F_Y(z))
$$

上述结论可以推广到 $n$ 个相互独立的随机变量：$M=\max(X_1,X_2,\cdots,X_n),N=\min(X_1,X_2,\cdots,X_n)$：

$$
F_M(z)=\prod_{i=1}^{n}F_{X_{i}}(z),1-F_N(z)=\prod_{i=1}^{n}(1-F_{X_i}(z))
$$

**分布函数的分布**

若随机变量 $\xi$ 的分布函数为 $F(x)=\mathrm{Pr}(\xi<x)$，因 $F(x)$ 非降，故可定义其反函数：

$$
F^{-1}(y)=\inf\{x|F(x)>y\}\qquad \forall y\in[0,1]
$$

对于随机变量 $\theta=F(\xi)$ 的分布，我们有：

$$
\mathrm{Pr}(\theta<x)=\mathrm{Pr}(F(\xi)<x)=\mathrm{Pr}(\xi <F^{-1}(x))=F(F^{-1}(x))=x
$$

故而 $\theta\sim U[0,1]$.

**注意**：这个结论反过来有更重要的应用意义：若 $\theta\sim U[0,1]$，对任意分布函数 $F(x)$，令 $\xi = F^{-1}(\theta)$，即可使得 $\xi$ 成为服从分布函数 $F(x)$ 的随机变量. 这样我们只要能生成 $\theta$，就能利用该变换生成 $\xi$，这是一种极其常见的采样方法.

![30172d9911d151d3740d4fed9660dbc6.png](30172d9911d151d3740d4fed9660dbc6.png)