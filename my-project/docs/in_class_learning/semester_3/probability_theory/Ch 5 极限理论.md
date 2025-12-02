# Ch.5 极限理论

### 大数定律

**依概率收敛**：设 $Y_1,Y_2,\cdots, Y_n, \cdots$ 为随机变量序列，若存在常数 $a$，对任意给定的 $\varepsilon > 0$，有：

$$
\lim_{n\to \infty}\mathrm{Pr}(|Y_n-a|\ge \varepsilon)=0
$$

或等价的

$$
\lim_{n\to\infty}\mathrm{Pr}(|Y_n-a|<\varepsilon)=1
$$

则称随机变量序列 $Y_1,Y_2,\cdots, Y_n, \cdots$ **依概率收敛于** $a$，记为 $Y_n\xrightarrow{P}a$.

**服从大数定律**：设 $X_1,X_2,\cdots,X_n,\cdots$ 为随机变量序列，若 $\forall \varepsilon>0$：

$$
\lim_{n\to\infty}\mathrm{Pr}\left(\left|\dfrac{1}{n}\sum_{k=1}^{n}X_k-\dfrac{1}{n}\sum_{k=1}^{n}\mathrm{E}X_k\right|\ge \varepsilon\right)=0
$$

或等价的

$$
\lim_{n\to\infty}\mathrm{Pr}\left(\left|\dfrac{1}{n}\sum_{k=1}^{n}X_k-\dfrac{1}{n}\sum_{k=1}^{n}\mathrm{E}X_k\right|< \varepsilon\right)=1
$$

则称 $\{X_n\}$ 服从大数定律.

以下介绍三个常用的大数定律：切比雪夫大数定律、独立同分布大数定律、伯努利大数定律.

**切比雪夫大数定律**：设 $X_1,X_2,\cdots$ 为两两不相关的随机变量序列，其方差一致有界（即存在常数 $C$ 使得 $\mathrm{Var}(X_k)<C$ 对一切 $k=1,2,\cdots$ 成立），则 $\{X_n\}$ 服从大数定律.

- proof.
    
    因 $\{X_n\}$ 两两不相关，即 $\mathrm{Cov}(X_i,X_j)=0$，故：
    
    $$
    \begin{aligned}
    \dfrac{1}{n^2}\mathrm{Var}\left(\sum_{k=1}^{n}X_k\right)
    &=\dfrac{1}{n^2}\left(\sum_{k=1}^{n}\mathrm{Var}X_k+2\sum_{1\le i<j\le n}\mathrm{Cov}(X_i,X_j)\right)\\
    &=\dfrac{1}{n^2}\sum_{k=1}^{n}\mathrm{Var}X_k\\
    &<\dfrac{1}{n^2}\times nC\\
    &=\dfrac{C}{n}\to 0
    \end{aligned}
    $$
    
    于是根据切比雪夫不等式：
    
    $$
    \begin{aligned}
    0&\le \mathrm{Pr}\left(\left|\dfrac{1}{n}\sum_{k=1}^{n}X_k-\dfrac{1}{n}\sum_{k=1}^{n}\mathrm{E}X_k\right|\ge \varepsilon\right)\\
    &=\mathrm{Pr}\left(\left|\dfrac{1}{n}\sum_{k=1}^{n}X_k-\mathrm{E}\left(\dfrac{1}{n}\sum_{k=1}^{n}X_k\right)\right|\ge \varepsilon\right)\\
    &\le \dfrac{1}{\varepsilon^2}\mathrm{Var}\left(\dfrac{1}{n}\sum_{k=1}^{n}X_k\right)\\
    &=\dfrac{1}{\varepsilon^2n^2}\mathrm{Var}\left(\sum_{k=1}^{n}X_k\right)\to 0\\
    \end{aligned}
    $$
    
    夹逼准则立得.
    

**独立同分布大数定律**：设 $X_1,X_2,\cdots$ 为相互独立且分布相同的随机变量序列，数学期望存在并记 $\mathrm{E}X_n=\mu$，则 $\{X_n\}$ 服从大数定律，即：

$$
\lim_{n\to \infty}\mathrm{Pr}\left(\left|\dfrac{1}{n}\sum_{k=1}^{n}X_k-\mu\right|\ge \varepsilon\right)=0
$$

**伯努利大数定律**：设 $n_A$ 是 $n$ 重伯努利试验中 $A$ 发生的次数，$A$ 发生的概率为 $p$，则 $\dfrac{n_A}{n}\xrightarrow{P}p$.

### 中心极限定理（Central Limit Theorem）

对于大量独立随机因素叠加而成的随机变量，其中每一个因素的影响很微小，那么这样的随机变量将大致服从正态分布，也即：

$$
\sum_{k=1}^{n}X_k\overset{\text{approximately}}\sim N\left(\mathrm{E}\left(\sum_{k=1}^{n}X_k\right),\mathrm{Var}\left(\sum_{k=1}^{n}X_k\right)\right)
$$

**标准化随机变量**：满足 $\mathrm{E}X=0,\mathrm{Var}X=1$ 的随机变量 $X$.

**随机变量标准化**：$X^*=\dfrac{X-\mathrm{E}X}{\sqrt{\mathrm{Var}X}}$.

**独立同分布中心极限定理**（Lindeberg-Levy CLT）：随机变量序列 $X_1,X_2,\cdots,X_n$ 独立同分布，记 $\mathrm{E}X_k=\mu,\mathrm{Var}X_k=\sigma^2,\sigma>0$，则对任意 $x$，有：

$$
\lim_{n\to\infty}\mathrm{Pr}\left(\dfrac{\sum_{k=1}^{n}X_k-n\mu}{\sqrt{n}\sigma}\le x\right)=\int_{-\infty}^{x}\dfrac{1}{\sqrt{2\pi}}\mathrm{e}^{-\frac{t^2}{2}}\mathrm{d}t=\Phi(x)
$$

**拉普拉斯中心极限定理**（de Moivre-Laplace theorem）：设 $\mu_n$ 是 $n$ 重伯努利试验中 $A$ 发生的次数，每次试验中 $A$ 发生的概率为 $p,q=1-p$，则对任意 $x$ 有：

$$
\lim_{n\to\infty}\mathrm{Pr}\left(\dfrac{\mu_n-np}{\sqrt{npq}}\le x\right)=\int_{-\infty}^{x}\dfrac{1}{\sqrt{2\pi}}\mathrm{e}^{-\frac{t^2}{2}}\mathrm{d}t=\Phi(x)
$$

推论：

$$
\mathrm{Pr}(a\le \mu_n\le b)=\Phi\left(\dfrac{b-np}{\sqrt{npq}}\right)-\Phi\left(\dfrac{a-np}{\sqrt{npq}}\right)
$$