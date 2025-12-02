# Ch.7 参数估计

参数估计与检验假设是统计推断的两个主要内容，参数估计的主要任务是在已知总体的情况下，利用样本构造合理的统计量对未知参数进行统计。对应非参数估计，七不知总体，只知道总体的某些特征。参数估计可分为点估计与区间估计。

**点估计的估计量和估计值**：设总体的分布为 $F(x;\theta)$，其中 $\theta=(\theta_1, \theta_2, \cdots, \theta_k)^\mathsf{T}$，根据样本 $X_1,X_2,\cdots, X_n$，构造统计量 $\hat{\theta}(X_1, X_2,\cdots, X_n)$ 作为 $\theta$ 的估计，称为 $\theta$ 的估计量。若 $x_1,x_2,\cdots, x_n$ 是一组样本观察值，代入 $\hat{\theta}$ 后得到的具体值称为 $\theta$ 的估计值，如此估计称为点估计。

### 矩估计（the method of moments）

矩估计：用样本矩作为总体矩的估计。设参数 $\theta=(\theta_1, \theta_2, \cdots, \theta_k)^\mathsf{T}$ 可作为总体矩 $\mu_1,\cdots,\mu_k$ 的函数 $\theta_i=h_i(\mu_1,\cdots,\mu_k),i=1,\cdots,k$，用样本矩 $A_1,\cdots,A_k$ 代替总体矩 $\mu_1,\cdots,\mu_k$ 所得的估计量就是**矩估计量**。

具体步骤如下：

1. 求总体的各阶原点矩 $\mu_i=g_i(\theta_1,\cdots,\theta_k)$
2. 解上述方程组得到 $\theta_i=h_i(\mu_1,\cdots,\mu_k)$
3. 用样本矩代替总体矩得到矩估计 $\hat{\theta}_i=h_i(A_1,\cdots,A_k)$.

**相合性/一致性（consistency）**：当样本容量充分大时，估计量可以以任一的精确程度逼近被估计参数的真值。相合性时一个估计量应具备的最基本性质，相合估计也称为一致估计、相容估计。按收敛意义不同，相合估计有弱相合估计、强相合估计等等。

矩估计的相合性：若 $h$ 为已知的连续函数，可以证明 $h(A_1,\cdots,A_k)\xrightarrow{P}h(\mu_1,\cdots,\mu_k)$.

矩估计是一种直观、简便的估计方法，适用范围很广，且不需要知道总体分布的具体类型，只需要知道总体矩的表达式即可。因未充分利用信息，矩估计往往精度不高。

习题：

1. 总体 $X\sim N(\mu,\sigma^2)$，$\mu$ 和 $\sigma^2$ 的矩估计分别为样本均值 $\bar{X}$ 和样本二阶中心矩 $S^{*2}$。
2. 总体 $X\sim U[\theta_1,\theta_2]$，$\theta_2$ 和 $\theta_1$ 的矩估计为 $\bar{X}\pm\sqrt{3}S^*$.
3. 总体 $X\sim \mathrm{Poisson}(\lambda)$，$\lambda$ 的矩估计为 $\bar{X}$.（事实上样本二阶中心矩也是一个矩估计，但是一般取阶数较低的）
4. 二维总体 $(X,Y)$ 的相关系数 $\rho$ 的矩估计是样本相关系数 $r$.

### 极大似然估计（MLE, maximum likelihood estimation）

极大似然估计由 Fisher 于 1922 年给出，是统计学中极为重要的方法。极大似然估计可作如下直观理解，有两个射手，一个技艺精湛，一个只是一般水平，现在我们发现有一枪射中了靶心，那么这枪可能是谁射的？我们应当选择技艺精湛的那个，因为其射中靶心的概率更大。

极大似然估计也称为最大似然估计，我国早期研究、教育借鉴苏联、日本，将其翻译为极大似然估计。然而极大似然估计取的是最大值点，在当下，最大、极大已严格区分，分别代表全局最大和局部最大的两种含义，下文将采用最大似然估计一词及其衍生词。

在已有样本的基础上，我们应选择参数的一个合理的估计值使得参数在取得该估计值时样本发生的可能性达到最大。

若设总体 $X$ 为连续型随机变量，其密度函数为 $p(x;\theta),\theta\in\Theta$，$\theta$ 为待估参数，$\Theta$ 为其取值范围。$(X_1,\cdots, X_n)$ 为来自总体 $X$ 的样本，因独立性，$(X_1,\cdots, X_n)$ 的概率密度为 $\prod_{i=1}^{n}p(x_i;\theta)$，又设 $(x_1,\cdots, x_n)$ 为样本的一组观察值，那么样本落在点 $(x_1,\cdots,x_n)$ 的领域内的概率就近似为 $\prod_{i=1}^{n}p(x_i;\theta)\mathrm{d}x_i$.

若设总体 $X$ 为离散型随机变量，其概率函数为 $p(x;\theta),\theta\in\Theta$. 设 $(X_1,\cdots, X_n)$ 为来自总体 $X$ 的样本，那么其联合概率仍然为 $\prod_{i=1}^{n}p(x_i;\theta)$.

无论 $X$ 如何，记 $L(x_1,\cdots,x_n;\theta)=\prod_{i=1}^{n}p(x_i;\theta)$

当样本值 $(x_1,\cdots,x_n)$ 取定时，上式为关于 $\theta$ 的函数，此时称为**似然函数**。满足下式的最大值点 $\hat{\theta}(x_1,\cdots,x_n)$ 称为 $\theta$ 的**最大似然估计值**，推广之得到 $\hat{\theta}(X_1,\cdots, X_n)$，称为**最大似然估计量**。

$$
L(x_1,\cdots,x_n;\theta)=\max_{\theta\in\Theta} L(x_1,\cdots,x_n;\theta)
$$

在实践中往往将求积的 $L(\theta)$ 通过单调的对数函数转化为求和的**对数似然函数** $\ln L(\theta)$，显然二者最大值点相同，于是称下式为**似然方程（组）**，解之往往得到最大似然估计。

$$
\sum_{i=1}^{n}\dfrac{\partial \ln p(x_i;\theta)}{\partial \theta}=0
$$

最大似然估计的**不变性原则**：设 $\hat{\theta}$ 是参数 $\theta$ 的最大似然估计，$\varphi(\theta)$ 有单值反函数，则 $\varphi(\hat{\theta)}$ 是 $\varphi(\theta)$ 的最大似然估计，也即

$$
\widehat{\varphi(\theta)}=\varphi(\hat{\theta})
$$

习题：

1. 总体 $X\sim B(1,p)$，$p$ 的最大似然估计是样本均值 $\bar{X}$.
2. 总体 $X\sim \mathrm{Poisson}(\lambda)$，$\lambda$ 的最大似然估计是样本均值 $\bar{X}$.
3. 总体 $X\sim N(\mu,\sigma^2)$，$\mu$ 和 $\sigma^2$ 的最大似然估计分别为 $\bar{X}$ 和 $S^{*2}$.
4. 总体 $X\sim U[\theta_1,\theta_2]$，\theta_1,\theta_2 的最大似然估计分别为 $\min(x_1,\cdots, x_n),\max\{x_1,\cdots,x_n\}$（提示：此时似然函数不连续，需按定义求得）

### 估计量的评价标准

此处仅介绍三种标准：**无偏性（unbiasedness）**、**均方误差准则（MMSE, minimum mean square error）**、**一致性（consistency）**。

翻译问题：均方误差准则通译实未确定，以下称呼其为更易理解的「最小均方误差准则」。「相合性」和「一致性」实际上是一个性质，英文也都是「consistency」，一个词为什么要搞两种翻译呢？鉴于一致性用到的依概率收敛和一致收敛实际上因后接词汇不同不会混淆，故而以下仍然称呼为一致性，实在有区分之必要时，会改用相合性，并说明和一致性同一。

**无偏性**：设 $\hat{\theta}(X_1,\cdots, X_n)$ 为参数 $\theta$ 的一个估计量，$\Theta$ 为其取值范围，若有

$$
\mathrm{E}(\hat{\theta}(X_1,\cdots,X_n)),\quad\forall \theta\in\Theta
$$

则称 $\hat{\theta}$  是 $\theta$ 的无偏估计量。

**渐进无偏估计**：我们知道方差存在且有限时，样本方差 $S^2$ 是总体方差 $\sigma^2$ 的无偏估计，但是样本二阶中心矩不是。然而 $\mathrm{E}(S^{*2})=\dfrac{n-1}{n}\sigma^2\to\sigma^2,n\to\infty$，这实际上也很好，称其为渐进无偏估计：估计不是无偏估计，但是在样本容量趋于无穷大时，期望极限等于参数。

**最小均方误差准则**：我们当然希望估计和真值越接近越好，我们记 $M(\hat{\theta},\theta)=\mathrm{E}(\hat{\theta}-\theta)$ 为均方误差，应最小化。

常见变形：$M(\hat{\theta},\theta)=\mathrm{Var}(\hat{\theta})-(\mathrm{E}(\hat{\theta})-\theta)^2$. 故而当估计为无偏估计时，均方误差变为统计量方差。

**一致性**：若有 $\hat{\theta}\xrightarrow{P}\theta$，则称 $\hat{\theta}$ 为 $\theta$ 的一致估计量。

### 区间估计

前面讨论的 $\hat{\theta}$ 都是一个值，称为点估计。现在我们要求给出一个区间 $(\hat{\theta}_1,\hat{\theta}_2)$ 来估计参数 $\theta$ 的范围，这称为区间估计。我们应当给出 $\theta$ 落在这个区间的概率有多大，这就引出了置信区间和置信度的概念。

定义：设 $\theta$ 是总体 $X$ 的未知参数，$X_1,\cdots, X_n$ 是来自总体 $X$ 的样本。若对于事先给定的常数 $\alpha(0<\alpha<1)$，存在两个统计量 $\hat{\theta}_1(X_1,\cdots, X_n)$ 和 $\hat{\theta}_2(X_1,\cdots, X_n)$ 有：$\mathrm{Pr}(\hat{\theta}_1<\theta<\hat{\theta})=1-\alpha$，则称 $(\hat{\theta}_1,\hat{\theta}_2)$ 是 $\theta$ 的置信度为 $1-\alpha$ 的**置信区间**，$\hat{\theta}_1,\hat{\theta}_2$ 分别成为**置信下限**和**置信上限**，$1-\alpha$ 称为**置信度**或**置信系数**。特别地，当 $\hat{\theta}_1\equiv -\infty$ 或 $\hat{\theta}_2\equiv \infty$ 时，称置信区间为单侧置信区间，对应置信上/下限称为单侧置信上/下限。

显然，置信区间的长度可以看作估计的精度，而精度往往和置信度不可兼得，在实际中，我们通常在保证置信度的前提下尽可能提高精度。

求区间估计的一般方法（**枢纽变量法**）：

​	(1) 先找一个样本函数 $U(X_1,\cdots,X_n;\theta)$，其包含待估参数 $\theta$，而不包含其他未知参数，且 $U$ 的分布已知，不依赖于任何未知参数，这样的参数称为**枢纽变量**，因含有未知参数 $\theta$ 故而不是统计量。

​	(2) 对实现给定的置信度为 $1-\alpha$，根据 $U$ 的分布找到两个常数 $a,b$ 使得：

$$
\mathrm{Pr}(a<U<b)=1-\alpha
$$

​	(3) 利用不等式变形，通过 $a<U<b$ 解得 $\hat{\theta}_1<\theta<\hat{\theta}_2$，$(\hat{\theta}_1,\hat{\theta}_2)$  即为所求。

习题：

- 总体 $X\sim N(\mu, \sigma^2)$，均值的置信区间。（已知总体方差取枢纽变量 $U=\dfrac{\bar{X}-\mu}{\sigma/\sqrt{n}}\sim N(0,1)$，不知总体方差取枢纽变量 $T=\dfrac{\sqrt{n}(\bar{X}-\mu)}{S}\sim t(n-1)$.）
- 总体 $X\sim N(\mu, \sigma^2)$，总体均值未知时，方差的置信区间。（取枢纽变量 $\dfrac{(n-1)S^2}{\sigma^2}\sim\chi^2(n-1)$.）

- 两个总体 $X\sim N(\mu_1,\sigma_1^2),Y\sim N(\mu_2,\sigma_2^2)$ 的均值差的置信区间：已知二者方差取枢纽变量

$$
   U=\dfrac{(\bar{X}-\bar{Y})-(\mu_1-\mu_2)}{\sqrt{\frac{\sigma_1^2}{n_1}+\frac{\sigma_2^2}{n_2}}}\sim N(0,1)
$$

   二者方差相等但未知取

$$
T=\sqrt{\dfrac{n_1n_2(n_1+n_2-2)}{n_1+n_2}}\cdot\dfrac{(\bar{X}-\bar{Y})-(\mu_1-\mu_2)}{\sqrt{(n_1-1)S_1^2+(n_2-1)S_2^2}}\sim t(n_1+n_2-2)
$$

   为枢纽变量。

- 两个总体 $X\sim N(\mu_1,\sigma_1^2),Y\sim N(\mu_2,\sigma_2^2)$ 的均值比的置信区间。当总体均值未知时，取 $F=\dfrac{S_1^2\sigma_2^2}{S_2^2\sigma_1^2}\sim F(n_1-1,n_2-1)$ 为枢纽变量。

- 非正态总体均值的区间估计（**大样本法**）：根据 CLT，转为 1.









