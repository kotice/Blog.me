# 整除理论与素数初步

## 声明
未经说明，本文讨论范围仅限于整数。

### 整除理论

#### 带余除法

对于给定的一个被除数 $a$, 和非零除数 $b$, 存在 $q, r$ 使得 $a = q \times b + r$, 其中 $r$ 满足 $r \in [0, b)$. 若 $r = 0$ 则称 $b$ 整除 $a$, 或 $a$ 被 $b$ 整除.记作 $b | a$.

基本定理: 对于任意的整数 $a, b\ (b \not = 0)$, 都存在 $q, r\ (r \in [0, b))$, 满足等式 $a = b \times q + r$.

#### 欧几里德算法

$$
gcd(a, b) = gcd(b, a\ mod\ b) 
$$ 

#### 裴蜀定理(贝祖定理)

$$
方程\ ax + by = d\ 有无穷多解当且仅当\ gcd(a, b) | d
$$

Proof: 考虑证明一个等价的形式 $ax + by = 1$ 有无穷多解当且仅当 $a, b$ 互质. 因为 $gcd(a, b) = 1$, 可得 $gcd(b, a\ mod\ b) = 1$.

不妨做带余除法, 并递归去做欧几里德算法.直到 $a\ mod\ b = 1$

$a = bq_1 + r_1$
$b = r_1q_2 + r_2$
$r_1 = r_2q_3 + r_3$
$r_{i} = r_{i + 1}q_{i + 2} + r_{i + 2}$
$r_{n - 1} = r_{n}q_{n + 1}$

此时 $x = q_{n +1}, y = 1$ 就是方程 $a'x + b'y = 1$ 的一组解. 直接回溯即可.
通解 $x = x' - kb, y = y' + ka$

#### 扩展欧几里德算法(exgcd)

$a\ mod\ b = a - \lfloor\frac{a}{b}\rfloor \times b$
$ax + by = 1, bx' + (a\ mod\ b)y' = 1$
$ax + by = bx' + (a - \lfloor\frac{a}{b}\rfloor)y'$

化简得

$x = y', y = x' - \lfloor\frac{a}{b}\rfloor y'$.

伪代码如下

$EXGCD\ (a,\ b,\ \&x,\ \&y)$
$1\ \ \ \ if\ \ b = 0$
$2\ \ \ \ \ \ \ \ \ \ x \leftarrow 1,\ y \leftarrow 0$
$3\ \ \ \ else$
$4\ \ \ \ \ \ \ \ \ EXGCD\ (b,\ a\ mod\ b,\ x,\ y)$
$5\ \ \ \ \ \ \ \ \  t \leftarrow x$
$6\ \ \ \ \ \ \ \ x \leftarrow y$
$7\ \ \ \ \ \ \ \ y \leftarrow t - \lfloor\frac{a}{b}\rfloor \times y$

### 素数

#### 算数基本定理

任何一个大于 $1$ 的整数都可以表示为 $\prod{p_k^{\alpha_i}}$

#### 约数相关

将 $p_k$ 互相组合, 所得乘积的集合即为该数除 $1$ 外的约数集. 考虑乘法原理, 有约数个数 $S = \prod(\alpha_i + 1)$.

对于约数和, 考虑构造一个多项式, 的质因数互相组合的去乘, 并使之相使所有加. 可以构造出 $S' = \prod\sum{(p_k^{\alpha_k} + 1)}$.

#### 无穷多素数的证明

对于调和级数 $f(n) = \sum_{i = 1}^\infty\frac{1}{i}$. 对于素数和 1, 可以直接用原数表示. 对于合数, 可以将其分解质因数. 这样我们可以像求约数和那样, 构造多项式, 将所有正整数表示出来.于是我们有:

$$
\sum_{i = 1}^\infty\frac{1}{i} = \prod\sum{(p_k^{\alpha_k} + 1)}
$$

假设素数是有限的, 等号右边的函数应有一个上确界. 而调和级数是发散的, 与假设矛盾. 故素数为无穷个成立.

#### 求素数

求 1 到 n 所有素数.

##### 试除法

对于每个数, 尝试所有 2 到 n / 2 的整数. 时间复杂度 $O(n^2)$.

##### 埃氏筛

每次遍历到一个没被筛过的数, 将其加入素数列表并将其倍数筛去. 时间复杂度 $O(n\ ln\ ln\ n)$.

##### 欧拉筛

埃氏筛的瓶颈在于有很多数被重复筛, 考虑每个数只用其最小质因子来筛. 时间复杂度 $O(n)$.伪代码如下.

$Euler\ (n)$
$1\ \ \ \ for\ \ i\ \ in\ \ 2..n$
$2\ \ \ \ \ \ \ \ \ \ if\ \ i\ \ isn't\ \ visited$
$3\ \ \ \ \ \ \ \ \ \ add\ \ i\ \ to\ \ prime\ \ number\ \ list$
$4\ \ \ \ \ \ \ \ \ \ for\ \ j\ \ in\ \ prime\ \ number\ \ list$
$5\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ if\ \ the\ \ minimum\ \ prime\ \ factor\ \ of\ \ i\ \ >=\ \ j$
$6\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ let\ \ i \times j\ \ be\ \ visited$






