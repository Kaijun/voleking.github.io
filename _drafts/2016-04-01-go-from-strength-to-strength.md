---
layout:     post
title:      "更进一步"
subtitle:   "《挑战程序设计竞赛》Summary"
date:       2016-04-01
author:     "Voleking"
header-img: "/img/"
catalog:    false
mathjax:    true
tags:
    -  ICPC
    -  Algorithms
---

# Tips #

1. 位移运算范围为 int
2. pow 返回浮点数可能会导致误差，慎用！！！
3. 样例数用 long long 可能会 TLE
4. 多组数据记得初始化
5. 小心过程量 overflow
6. Type convertions
7. 图未清零
8. 在取余的情况下，要避免减法运算的结果出现负数 (...+ MOD) % MOD;
9.  

## Basic Algorithm ##


### Sort ###

+ Bubble Sort  
```c++ 
for (int i = 0; i < N; i++)
    for (int j = 0; j < N - i - 1; j++)
        if (A[j] > A[j + 1]) swap(A[j], A[j + 1]);
```

+ Insertion Sort  
```c++
for (int i = 1; i < N; i++) {
    int tmp = A[i], j;
    for (j = i - 1; j >= 0 && A[j] > tmp; j--)
        A[j + 1] = A[j];
    A[++j] = tmp; 
}
```

+ Selection Sort
```c++
for (int i = 0; i < N; i++)
    for (int j = i + 1; j < N; j++)
        if (A[i] > A[j]) swap(A[i], A[j])
```

+ Merge Sort
```c++
void merge_sort(int A[], int l, int r) {
    if (l >= r) return ;
    int mid = (l + r) / 2;
    merge_sort(A, l, mid);
    merge_sort(A, mid + 1, r); 
    int i, j, k;
    i = l; j = mid + 1; k = l;
    while (i <= mid && j <= r) {
        if (A[i] < A[j]) {
            B[k] = A[i++];
        }
        else {
            B[k] = A[j++];
        }
        k++;
    }
    while (i <= mid) {
        B[k] = A[i++];
        k++;
    }
    while (j <= r) {
        B[k] = A[j++];
        k++;
    }
    memcpy(A, B, r - l + 1);
    return ; 
}
```

+ Quick Sort
```c++   
void quicksort(int A[], int l, int r) {
    int i = l, j = r, mid = A[(r - l) / 2 + l];
    while (i <= j) {
        while (A[i] < mid) i++;
        while (A[j] > mid) j--;
        if (i <= j) {
            swap(A[i], A[j]);
            ++i; --j;
        }
    }
    if (i < r) quicksort(A, i, r);
    if (l < j) quicksort(A, l, j);        
    return ;
}
```

+ Heap Sort  
    * 见堆的内容


### DP ###

#### LIS ####

```c++
int dp[MAX_N], A[MAX_N];
long lis(int n) {
    int dp[MAX_N];
    fill(dp, dp + n, INF);
    for (int i = 0; i < n; ++i)
        *lower_bound(dp, dp + n, A[i]) = A[i];// lds: -A[i]; ln: upper_bound
    return lower_bound(dp, dp + n, INF) - dp;
}
```

#### Knapsack Problem ####

* 0/1 背包

$$f[i, j] = max(f[i - 1, j], f[i - 1, j - w[i]] + v[i])$$

```c++
for (int i = 0; i < N; ++i)
    for (int j = W; j >= w[i]; --j)
        f[j] = max(f[j - w[i]] + c[i], f[j]);
```

* 完全背包

$$f[i, j] = max(f[i - 1, j], f[i - 1, j - w[i]] + j[i])$$

```c++
for (int i = 0; i < N; ++i)
    for (int j = w[i]; j <= W; ++j)
        f[j] = max(f[j - w[i]] + c[i], f[v]);
```

注意循环顺序的不同背后思路。  

+ 一个简单的优化：若两件物品 i、j 满足 $w[i] ≤ w[j]$ 且 $c[i] ≥ c[j]$，则讲物品 j 去掉，不用考虑。  
+ 转化为 01 背包问题求解：  
    * 第 i 种物品转化为 $\frac{V}{w[i]}$ 件费用于价值均不变的物品。  
    * 第 i 种物品拆成费用为 $w[i] * 2^k$，价值为 $c[i] * 2^k$ 的若干件物品其中 k 满足 $w[i] * 2^k < V$

* 多重背包

$$f[i, j] = max(f[i - 1, j - w[i] * k] + v[i] * k | 0 <= k <= m[i])$$

+ 优化：转化为 01 背包问题  
    * 将第 i 件物品分成若干件物品，每件物品的系数分别为：$1,2,4,\ldots,2^{(k - 1)},n[i]-2^k$
    * ** 根据 w，v 范围改变 DP 对象，可以考虑针对不同价值计算最小的重量。（ $f[i][j]$，其中 j 代表价值总和）**

```c++
for (int i = 0; i < N; ++i) {
    int num = m[i];
    for (int k = 1; num > 0; k <<= 1) {
        int mul = min(k, num);
        for (int j = W; j >= w[i] * mul; --j) {
            f[j] = max(f[j - w[i] * mul] + v[i] * mul, f[j]);
        }
        num -= mul;
    }
}
```

* 混合三种背包

&emsp;&emsp;弄清楚上面三种背包后分情况就好  

* 二维费用背包

$$f[i, j, k] = max(f[i - 1, j, k], f[i - 1, j - a[i], k - b[i]] + c[i])$$

二维费用可由最多取 m 件等方式隐蔽给出。  

* 分组背包

$$f[k, j] = max{f[k - 1, j], f[k - 1, j - w[i]] + v[i] | i \in K})$$

```c++
for (int k = 0; k < K; ++k)
    for (j = W; j >= 0; --j)
        for (int i = 0; i <= m[k]; ++i)
            f[j] = max(f[j - w[i]] + v[i], f[j]);
```

显然可以对每组中物品应用完全背包中“一个简单有效的优化”  

* 有依赖背包

由 NOIP2006 金明的预算方案引申，对每个附件先做一个 01 背包，再与组件得到一个 $V - w[i] + 1$ 个物品组。  
更一般问题，依赖关系由「森林」形式给出，涉及到树形 DP 以及泛化物品，这里不表。  

* 背包问题方案总数

$$f[i, j] = sum{f[i - 1, j], f[i - 1, j - w[i]] + v[i]},f[0, 0] = 0$$

>>更多内容详见「背包九讲」

#### Maximum Subarray Sum ####
```c++
int max_subarray_sum(int A[], int n) {
    int res, cur;
    if (!A || n <= 0) return 0; 
    res = cur = a[0];
    for (int i = 0; i < n; ++i) {
        if (cur < 0) cur = a[i];
        else cur += a[i];
        res = max(cur, res);
    }
    return res;
}
```

### Set ###

```c++
// 子集枚举
int sub = sup;
do {
    sub = (sub - 1) & sup;
} while (sub != sup); // -1 & sup = sup;

// 势为 k 的集合枚举
int comb = (1 << k) - 1;
while (comb < 1 << n) {
    int x = comb & -comb, y = comb + x;
    comb = ((comb & ~y) / x >> 1) | y;
}

do {

} while (next_permutation(A, A + N));
```


---



## Data Structure ##

* Heap 
```c++
int heap[MAX_N], sz = 0;
void push(int x) {
    int i = sz++;

    while (i > 0) {
        int p = (i - 1) / 2;
        if (heap[p] <= x) break;
        heap[p] = heap[i];
        i = p;
    }
    heap[i] = x;
}
int pop() {
    int ret = heap[0];
    int x = heap[--sz];
    int i = 0;
    while (i * 2 + 1 < sz) {
        int a = i * 2 + 1, b = i * 2 + 2;
        if (b < sz && heap[b] < heap[a]) a = b;
        if (heap[a] >= x) break;
        heap[i] = heap[a];
        i = a;
    }
    heap[i] = x;
    return ret;
}
```

* Binary Search Tree
```c++
struct node {
    int val;
    node *lch, rch;
};

node *insert(node *p, int x) {
    if (p == NULL) {
        node *q = new node;
        q->val = x;
        q->lch = q->rch = NULL;
        return q;
    } else {
        if (x < p->val) p->lch = insert(p->lch, x);
        else p->rch = insert(p->rch, x);
        return p;
    }
}
bool find(node *p, int x) {
    if (p == NULL) return false;
    else if (x == p->val) return true;
    else if (x < p->val) return find(p->lch, x);
    else return find(p->rch, x);
}
node *remove(node *p, int x) {
    if (p == NULL) return NULL;
    else if (x < p->val) p->lch = remove(p->lch, x);
    else if (x > p->val) p->rch = remove(p->rch, x);
    else if (p->lch == NULL) {
        node *q = p->rch;
        delete p;
        return q;
    } else if (p->lch->rch == NULL) {
        node *q = p->lch;
        q->rch = p->rch;
        delete p;
        return q;
    }  else {
        // 把左儿子子孙中最大的节点提到需要删除的节点上
        node *q;
        for (q = p->lch; q->rch->rch != NULL; q = q->rch);
        node *r = q->rch;
        q->rch = r->lch;
        r->lch = p->lch;
        r->rch = p->rch;
        delete p;
        return r;
    }
    return p;
}
```

* Union-find Set  
```c++
int par[MAX_N];
int rnk[MAX_N];

void init(int n) {
    for (int i = 0; i < n; ++i) {
        par[i] = i;
        rnk[i] = 0;
    }
}
int find(int x) {
    return par[x] == x? x : par[x] = find(par[x]);
}
bool same(int a, int b) {
    return find(a) == find(b);
}
void unite(int x, int y) {
    x = find(x);
    y = find(y);
    if (x == y) return;
    if (rnk[x] < rnk[y]) {
        par[x] = y;
    } else {
        par[y] = x;
        if (rnk[x] == rnk[y]) rnk[x]++;
    }
}
```

**当然，更快捷简单的做法，是使用 C++ 的 container。**



## Graph ##

```c++
struct edge {
    int from;
    int to, dis;
};
vector<edge> G[MAX_V];
vector<edge> es;
bool vis[MAX_V];
int dist[MAX_N], V, E, pre[MAX_V];
int cost[MAX_V][MAX_V];
```

* Shortest Way
```c++
void dijkstra(int s) {
    priority_queue<Pii, vector<Pii>, greater<Pii> > que;// fisrt 是最短距离，second 是顶点编号
    fill(dist, dist + V, INF);
    dist[s] = 0; que.push(Pii(0, s));
    while (!que.empty()) {
        Pii p = que.top(); que.pop();
        int v = p.second;
        if (dist[v] < p.first) continue;
        for (int i = 0; i < G[v].size(); i++) {
            edge e = G[v][i];
            if (dist[e.to] > dist[v] + e.dis) {
                dist[e.to] = dist[v] + e.dis;
                que.push(Pii(dist[e.to], e.to));
            }
        }
    } 
}
void bellman_ford(int s) {
    fill(dist, dist + V, INF);
    dist[s] = 0;
    while (true) {
        bool update = false;
        for (int i = 0; i < E; ++i) {
            edge e = es[i];
            if (dist[e.from] != INF && dist[e.from] + e.dis < dist[e.to]) {
                update = true;
                dist[e.to] = dist[e.from] + e.dis;
            }
        }
        if (!update) break;
    }
}
void spfa(int s) {
    queue<int> que;
    fill(dist, dist + V, INF);
    fill(vis, vis + V, false);
    dist[s] = 0; que.push(s); vis[s] = true;
    while (!que.empty()) {
        int v = que.front(); que.pop();
        vis[v] = false;
        for (int i = 0; i < G[v].size(); ++i) {
            int u = G[v][i].to;
            if (dist[u] > dist[v] + G[v][i].dis) {
                dist[u] = dist[v] + G[v][i].dis;
                if (!vis[u]) {
                    que.push(u);
                    vis[u] = true;
                }
            }
        }
    }
}
```

* Spanning Tree
```c++
int prime() {
    fill(dist, dist + V, INF);
    fill(vis, vis + V, false);
    dist[0] = 0;
    int res = 0;
    while (true) {
        int v = -1;
        for (int u = 0; u < V; ++u) {
            if(!vis[u] && (v == -1 || dist[u] < dist[v])) v = u;
        }
        if (v == -1) break;
        vis[v] = true;
        res += dist[v];
        for (int u = 0; u < V; u++)
            dist[u] = min(dist[u], cost[v][u]);
    }
    /*
    priority_queue<Pii, vector<Pii>, greater<Pii> > que;
    int res;
    fill(dist, dist + V, INF);
    fill(vis, vis + V, false);
    res = dist[0] = 0;
    que.push(Pii(0, s));
    while (!que.empty()) {
        Pii p = que.top(); que.pop();
        int v = p.second;
        if (used[v] || dist[v] < p.first) continue;
        res += dist[v];
        for (int i = 0; i < G[v].size(); ++i) {
            edge e = g[v][i];
            if (dist[e.to] > e.dis) {
                dist[e.to] = e.dis;
                que.push(Pii(dist[e.to], e.to));
            }
        }
    }
    */
    return res;
}
bool cmp(edge &e1, edge &e2) {
    return e1.dis < e2.dis;
}
int kruskal() {
    sort(es.begin(), es.end(), cmp);
    init(V);
    int res = 0;
    for (int i = 0; i < E; ++i) {
        edge e = es[i];
        if (!same(e.from, e.to)) {
            unite(e.from, e.to);
            res += e.dis;
        }
    }
    return res;
}
```


--- 



## Math Problem ##

```c++
template<typename T> T gcd(T a, T b) {
    //return (b)? gcd(b, a  % b) : a;
    while (b) { T t = a % b; a = b; b = t; } return a;
}
template<typename T> T lcm(T a, T b) { 
    return a / gcd(a, b) * b;
}
// find (x, y) s.t. a x + b y = gcd(a, b) = d
template<typename T> T exgcd(T a, T b, T &x, T &y) { 
    T d = a; 
    if (b) { 
        d = exgcd(b, a % b, y, x); 
        y -= a / b * x; 
    } else { 
        x = 1; y = 0; 
    } 
    return d;
}
template<typename T> T mod_inverse(T a, T m) {
    T x, y;
    exgcd(a, m, x, y);
    return (m + x % m) % m;
}

ll CRT(vector<ll> &a, vector<ll> &m) {
    ll M = 1LL, res = 0;
    for (int i = 0; i < m.size(); ++i)
        M *= m[i];
    for (int i = 0; i < m.size(); ++i) {
        ll Mi, Ti;
        Mi = M / m[i]; Ti = mod_inverse(Mi, mi);
        res = (res + a[i] * (Mi * Ti) % M) % M;
    }
    return res;
}
ll mod_pow(ll x, ll n, ll mod) { 
    ll res = 1;
    while (n > 0) {
        if (n & 1) res = res * x % mod;
        x = x * x % mod;
        n >>= 1;
    }
    return res;
    // return b ? qpow(a * a % mod, b >> 1, mod) * (b & 1 ? a : 1) % mod : 1;
}

// some function about prime
bool isprime(int n) {
    for (int i = 2; i * i <= n; ++i)
        if (n % i == 0) return false;
    return n != 1;
}
vector<int> divisor(int n) {
    vector<int> res;
    for (int i = 1; i * i <= n; ++i) {
        if (n % i == 0) {
            res.push_back(i);
            if (i != n / i) res.push_back(n / i);
        }
    }
    return res;
}
map<int, int> prime_factor(int n) {
    map<int, int> res;
    for (int i = 2; i * i <= n; ++i) {
        while (n % i == 0) {
            ++res[i];
            n /= i;
        }
    }
    if (n != 1) res[n] = 1;
    return res;
}
int prime[MAX_N];
bool isPrime[MAX_N + 1];
int seive(int n) {
    int p = 0;
    fill(isPrime, isPrime + n + 1, true);
    isPrime[0] = isPrime[1] = false;
    for (int i = 2; i <= n; ++i) 
        if (isPrime[i]) {
            prime[p++] = i;
            for (int j = 2 * i; j <= n; j += i) isPrime[j] = false;
        }
    return p;
}
// the number of prime in [L, r)
// 对区间 [l, r）内的整数执行筛法，prime[i - l] = true <=> i 是素数
bool segPrimeSmall[MAX_L];
bool segPrime[MAX_SQRT_R];
void segment_sieve(ll l, ll r) {
    for (int i = 0; (ll)i * i < r; ++i) segPrimeSmall[i] = true;
    for (int i = 0; i < r - l; ++i) segPrime[i] = true;
    for (int i = 2; (ll)i * i < r; ++i) {
        if (segPrimeSmall[i]) {
            for (int j = 2 * i; (ll)j * j <= r; j += i) segPrimeSmall[j] = false;
            for (ll j = max(2LL, (l + i - 1) / i) * i; j < r; j += i) segPrime[j - l] = false;
        }
    }
}
// returning count of nk in range [l, r]
template<typename T> T mps(T l, T r, T k) { 
    return ((r - (r % k + k) % k) - (l + (k - l % k) % k)) / k + 1;
}
```

+ Moebius 
```c++
int mu[MAX_N];
void moebius() {
    int cnt = 0; mu[1] = 1;
    memset(vis, 0, sizeof vis);
    for (int i = 2; i < MAX_N; ++i) {
        if (!vis[i]) {
            prime[cnt++] = i;
            mu[i] = -1;
        }
        for (int j = 0; j < cnt && i * prime[j] < MAX_N; ++j) {
            vis[i * prime[j]] = true;
            if (i % prime[j])
                mu[i * prime[j]] = -mu[i];
            else 
                mu[i * prime[j]] = 0, break;
        }
    }
}
```

# String #

最小最大表示法：
```c++
int getMinString(const string &s) {  
    int len = (int)s.length();
    int i = 0, j = 1, k = 0;  
    while(i < len && j < len && k < len) {
        int t = s[(i+k)%len] - s[(j+k)%len];
        if(t == 0) k++;
        else {
            if(t > 0) i += k + 1;//getMaxString: t < 0
            else j += k + 1;
            if(i==j) j++;
            k = 0;
        }
    }
    return min(i,j);
}
```

KMP
```c++
int nxt[MAX_N];
void getNext(const string &str) {
    int len = str.length();
    int j = 0, k;
    k = nxt[0] = -1;
    while (j < len) {
        if (k == -1 || str[j] == str[k]) 
            nxt[++j] = ++k;
        else k = nxt[k];
    }
}
int kmp(const string &tar, const string &pat) {
    getNext(pat);
    int num, j, k;
    int lenT = tar.length(), lenP = pat.length();
    num = j = k = 0;
    while (j < lenT) {
        if(k == -1 || tar[j] == pat[k])
            j++, k++;
        else k = nxt[k];
        if(k == lenP) {
            // res = max(res, j - lenP);
            k = nxt[k];
            ++num;
        }
    }
    return num;//lenP - res - 1;
}
```

