# Ch.1 随机事件与概率

### 一、随机试验与随机事件（P1）

**随机试验**：对随机现象的依次观测.

特点：

①在相同的条件下试验可重复进行.

②每次实验具有多种结果，但试验之前可知道试验的所有可能结果.

③每次试验会出现这些可能结果之一，但试验前不能确定哪一个结果会出现.

在随机试验 $E$ 中，把所有可能结果的集合称为**样本空间**，记为 $\Omega$. 样本空间的元素，即 $E$ 的每个可能结果称为**基本事件**或**样本点**，记为 $e$.

**随机事件**：可能发生也可能不发生的事件. 可定义为：样本空间 $\varOmega$ 的子集，常常记为 $A, B, C$ 等，随机事件可简称为**事件**.

两个特殊的事件：**必然事件**，**不可能事件**.

必然事件：样本空间 $\varOmega$.

不可能事件：空集 $\varPhi$.

### 二、事件间的关系及运算（P2）

以下设 $\varOmega$ 是给定的样本空间，此样本空间上的随机事件为 $A, B, C, A_k(k=1, 2, \cdots)$ 等.

**包含关系**：如果事件 $A$ 发生必导致事件 $B$ 发生，则称事件 $B$ 包含事件 $A$，记 $B\supset A$.

**互不相容关系/互斥关系**：若事件 $A$ 与事件 $B$ 不可能同时发生，则称 $A, B$ 互不相容（或互斥），此时二者没有共同的样本点.

**相等关系**：若 $B\supset A$，且 $A\supset B$，则称 $A$ 与 $B$ 相等，记为 $A=B$，此时两事件的样本点完全相同.

**事件的并**：事件 $A$ 与 $B$ 至少发生一个所构成的事件称为 $A$ 与 $B$ 的并，记为 $A\cup B$，其样本点由 $A$ 与 $B$ 的样本点合并而成.

事件 $A_1, A_2, \cdots, A_n$ 至少发生一个的事件称为 $A_1, A_2, \cdots, A_n$ 的并，记为 $A_1\cup A_2\cup \cdots \cup A_n$ 或 $\bigcup_{i=1}^{n} A_i$.

**事件的交**：事件 $A$ 与 $B$ 同时发生的事件称为 $A$ 与 $B$ 的交，记为 $A\cap B$ 或 $AB$，其样本点由 $A$ 与 $B$ 共同的样本点组成.

事件 $A_1, A_2, \cdots, A_n$ 同时发生的事件称为 $A_1, A_2, \cdots, A_n$ 的交，记为 $A_1\cap A_2\cap \cdots \cap A_n$ 或 $\bigcap_{i=1}^{n} A_i$ 或 $A_1A_2\cdots A_n$.

**事件的差**：事件 $A$ 发生而事件 $B$ 不发生的事件称为 $A$ 与 $B$ 的差，记为 $A-B$，其样本点由 $A$ 中除去 $B$ 的样本点组成.

**对立事件**：事件 $A$ 不发生的事件称为 $A$ 的对立事件，即为 $\overline{A}$，其由 $\Omega$ 中除 $A$ 以外的样本点组成.

注意如下等式：

1. $A=(A-B)\cup (AB)$.
2. $A\cup B=A\cup (B-A)=(A-B)\cup (AB)\cup (B-A)$.
3. $A-B=A-(AB)=A\overline{B}$
4. $\overline{A}=\Omega -A, A\cup \overline{A}=\Omega$.

可以证明事件的运算满足以下的运算律：

1. **交换律**：$A\cup B=B\cup A, A\cap B = B\cap A$.
2. **结合律**：$(A\cup B)\cup C=A\cup(B\cup C), (A\cap B)\cap C=A\cap(B\cap C$).
3. **分配律**：$A\cup(B\cap C)=(A\cup B)\cap (A\cup C), A\cap (B\cup C)=(A\cap B)\cup(A\cap C)$.
4. **德摩根律(De Morgan’s laws)**：$\overline{A\cup B}=\overline{A}\cap \overline{B}, \overline{A\cap B}=\overline{A}\cup \overline{B}$.
    
    可以推广：
    
    $$
    \overline{\bigcup_{i=1}^{n}A_i}=\bigcap_{i=1}^{n}\overline{A_i}, \overline{\bigcap_{i=1}^{n}A_i}=\bigcup_{i=1}^{n}\overline{A_i}
    $$
    

### 三、频率与概率（P4）

设随机事件 $A$ 在 $n$ 次重复试验中共出现 $n_A$ 次，定义 $A$ 发生的**频率**如下，并记为 $f_n(A)$.

$$
f_n(A)=\dfrac{n_A}{n}
$$

事件 A 的频率具有如下性质：

1. $0\leqslant f_n(A)\leqslant 1$.
2. $f_n(\varOmega)=1$.
3. 若 $A_1, A_2, \cdots, A_n$ 互不相融，则
    
    $$
    f_n\left(\bigcup_{i=1}^{n} A_i\right)=\sum_{i=1}^{n}f_n(A_i)
    $$
    

**频率的稳定性**：在 $n$ 次试验中，随着试验次数 $n$ 的增加，事件的频率将在某个数值 $p$ 附近稳定地摆动，一般来说，$n$ 越大，摆动的幅度越小，此数值可定义为 $A$ 发生地概率，称为**统计概率**.

1933 年，苏联数学家**柯尔莫哥洛夫(Kolmogorov)**提出了概率的公理化定义，通过规定概率应具有的基本性质来定义概率，由此建立了概率论的理论体系.

**概率**的公理化定义【Def. 1.1】：设 $E$ 是随机试验，$\Omega$ 为其样本空间. 对于 $E$ 的每一个随机事件 $A$，对应一个实数 $\mathrm{Pr}(A)$，如果集合函数 $\mathrm{Pr}(\cdot)$ 满足如下条件，则称 $\mathrm{Pr}(A)$ 为事件 $A$ 的概率：

1. 非负性：$\mathrm{Pr}(A)\geqslant 0$.
2. 规范性：$\mathrm{Pr}(\varOmega)=1$.
3. 可列可加性：若 $A_1, A_2, \cdots A_n, \cdots$ 两两互不相容，则
    
    $$
    \mathrm{Pr}\left(\bigcup_{i=1}^{\infty} A_i\right)=\sum_{i=1}^{\infty}\mathrm{Pr}(A_i)
    $$
    

概率的一些性质：

1. $\mathrm{Pr}(\varPhi)=0$.
    
    proof. Trivial. (P6)
    
2. 若 $A_1, A_2, \cdots A_n$ 两两互不相容，则
    
    $$
    \mathrm{Pr}\left(\bigcup_{i=1}^{n} A_i\right)=\sum_{i=1}^{n}\mathrm{Pr}(A_i)
    $$
    
    proof. Trivial. (P6)
    
3. 对任意两事件 $A, B$，有 $\mathrm{Pr}(A-B)=\mathrm{Pr}(A)-\mathrm{Pr}(AB)$.
    
    proof. Trivial. (P6)
    
4. 对任意两事件 $A,B$，有**加法定理**：
    
    $$
    \mathrm{Pr}(A\cup B)=\mathrm{Pr}(A)+\mathrm{Pr}(B)-\mathrm{Pr}(AB)
    $$
    
    proof. Trivial. (P6)
    
    利用归纳法，可推广到 $n$ 个事件的加法定理：
    
    $$
    \mathrm{Pr}\left(\bigcup_{i=1}^{n} A_i\right)=\sum_{i=1}^{n}(-1)^{i-1}\sum_{1\leqslant a_1<a_2<\cdots<a_i\leqslant n}\mathrm{Pr}\left(\bigcap_{j=1}^{i}A_j\right)
    $$
    
5. 对任意事件 $A$，有 $\mathrm{Pr}\left(\overline{A}\right)=1-\mathrm{Pr}(A)$.
    
    proof. Trivial. (P7)
    

**等可能概型/古典概型**：具有如下特点的一类随机试验：

1. 样本空间 $\varOmega$ 的样本点个数为有限个.
2. 样本空间中的每个基本事件/样本点发生的可能性相同.

其为概率论发展初期的主要研究对象，故称为古典概型.

特点：

设随机试验 $E$ 为等可能概型，若其样本空间 $\varOmega$ 含有 $n$ 个样本点，而事件 A 含有 $m$ 个样本点，则事件 $A$ 的概率为 $\mathrm{Pr}(A)=\dfrac{m}{n}$.

**抽签原理**：袋中有 $a$ 只白球，$b$ 只红球，若干人依次从中各取一球，取后不妨会，则任一人取得红球的概率相等，都是 $\dfrac{a}{a+b}$.

**几何概率**：若随机试验的样本空间 $\varOmega$ 对应一个度量有限的几何区域 S，且所有的基本事件与 $S$ 内的点一一对应，则任一随机事件 $A$ 对应 $\varOmega$ 中的某一子区域 $D$. 若事件 $A$ 的概率只和 $A$ 对应的区域 $D$ 的度量成正比，与 $D$ 的形状及 $D$ 在 $S$ 中的位置无关，则 $A$ 发生的概率定义为 $\mathrm{Pr}(A)=\dfrac{m(A)}{m(\varOmega)}$，其中 $m(X)$ 为 $X$ 对应区域的度量. 

### 四、条件概率（P12）

定义：某事件 $A$ 在另一事件 $B$ 发生情况之下发生的概率，记作 $\mathrm{Pr}(A|B)$.

公理化定义：设 $A,B$ 为两个随机事件，$P(B)>0$，称 $\mathrm{Pr}(A|B)=\dfrac{\mathrm{Pr}(AB)}{\mathrm{Pr}(B)}$ 为在事件 $B$ 发生的条件之下，事件 $A$ 发生的概率. 

性质：容易验证条件概率 $\mathrm{Pr}(\cdot|B)$ 满足概率定义的三个条件：非负性、规范性、可列可加性.

**乘法公式**：条件概率定义变形：$\mathrm{Pr}(AB)=\mathrm{Pr}(B)\mathrm{Pr}(A|B)$.

当然其可以反过来：$\mathrm{Pr}(AB)=\mathrm{Pr}(A)\mathrm{Pr}(B|A)$.

当然其可以再对 $B$ 进行展开，得到多元版本：

$$
\mathrm{Pr}(A_1A_2\cdots A_n)=\mathrm{Pr}(A_1)\mathrm{Pr}(A_2|A_1)\mathrm{Pr}(A_3|A_1A_2)\cdots\mathrm{Pr}(A_n|A_1A_2\cdots A_{n-1})
$$

**划分/完备事件组**：若 $n$ 个事件 $A_1,A_2,\cdots,A_n$ 满足

(1) $A_1,A_2,\cdots,A_n$ 两两互不相容.

(2) . .

则称 $A_1,A_2,\cdots,A_n$ 为样本空间 $\varOmega$ 的一个划分或完备事件组. 在随机试验的每次试验中，$A_1,A_2,\cdots,A_n$ 必发生一个且仅发生一个.

**全概率公式**：设 $A_1, A_2,\cdots, A_n$ 为完备事件组，则对事件 $B$ 有：

$$
\mathrm{Pr}(B)=\sum_{k=1}^{n}\mathrm{Pr}(A_k)\mathrm{Pr}(B|A_k)
$$

**贝叶斯公式**：设 $A_1, A_2,\cdots, A_n$ 为完备事件组，则对事件 $B$ 有

$$
\mathrm{Pr}(A_i|B)=\dfrac{\mathrm{Pr}(A_i)\mathrm{Pr}(B|A_i)}{\sum_{k=1}^{n}\mathrm{Pr}(A_k)\mathrm{Pr}(B|A_k)}
$$

### 五、独立性（P18）

**独立性**：设 $A,B$ 是两个随机事件，若满足 $\mathrm{Pr}(AB)=\mathrm{Pr}(A)\mathrm{Pr}(B)$，则称事件 $A,B$ 相互独立，简称 $A,B$ 独立.

**多个事件的独立性**：

三个事件的独立性：设 $A,B,C$ 是三个随机事件，若：

$$
\begin{cases}
\mathrm{Pr}(AB)=\mathrm{Pr}(A)\mathrm{Pr}(B)\\
\mathrm{Pr}(BC)=\mathrm{Pr}(B)\mathrm{Pr}(C)\\
\mathrm{Pr}(CA)=\mathrm{Pr}(C)\mathrm{Pr}(A)\\
\mathrm{Pr}(ABC)=\mathrm{Pr}(A)\mathrm{Pr}(B)\mathrm{Pr}(C)
\end{cases}
$$

则称三事件相互独立，注意这和三事件两两独立有区别.

$n$ 个事件的独立性：设 $A_1,A_2,\cdots,A_n$ 为 $n$ 个随机事件.

$$
\mathrm{Pr}(A_{i_1}A_{i_2}\cdots A_{i_k})=\mathrm{Pr}(A_{i_1})\mathrm{Pr}(A_{i_2})\cdots\mathrm{Pr}(A_{i_k}),\\1\le i_1<i_2<\cdots<i_k\le n,k=2,3,\cdots,n
$$

则称事件 $A_1,A_2,\cdots,A_k$ 相互独立.

**分组独立性定理**：设事件 $A_1,A_2,\cdots,A_n$ 相互独立，将其任意分为没有公共事件的 $k$ 个组，每个组任意作事件运算，得到共 $k$ 个新事件，则这 $k$ 个新事件相互独立.

**小概率事件原理**：设随机试验中某事件 $A$ 发生的概率为 $p$，无论 $p>0$ 多么小，只要不断独立重复地做 $n$ 次试验，$A$ 迟早会发生的概率为 $1$，其只因 $(1-p)^n\to 1$ 当 $n\to +\infty$.

可靠性分析：一个元件或一个系统的可靠性是指其正常工作的概率，可靠性分析需要讨论按一定方式连接的多个独立元件或子系统正常工作的概率，连接方式有串联、并联与串并联混合. 串联则需要所有元件均正常工作，即事件交；并联只需所有元件不全不正常工作，即事件并.

$n$ **重伯努利试验**：是一类重要的独立重复试验概型，其具有如下两个特点：

(1) 每次试验只有两个结果，$A$ 与 $\overline{A}$，且 $\mathrm{Pr}(A)=p, \mathrm{Pr}(\overline{A})=1-p=q$.

(2) 试验进行 $n$ 次，每次试验的结果相互独立.

**泊松定理**：设 $n$ 为正整数，$\lambda = np_n$ 为常数，则对任意正整数 $k$ 有：

$$
\lim_{n\to \infty}\binom{n}{k}{p_n}^{k}(1-p_n)^{n-k}=\dfrac{\lambda^k}{k!}\mathrm{e}^{-\lambda}
$$