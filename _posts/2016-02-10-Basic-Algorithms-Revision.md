---
layout:     post
title:      "Basic Algorithms Revision"
subtitle:   "《Free Pascal 语言与基础算法》小结"
date:       2016-03-26
author:     "Voleking"
header-img: "http://7xqllw.com1.z0.glb.clouddn.com/post-Algorithms.jpg"
mathjax:    true
tags:
    - ICPC
    - Algorithms
    - 
---

>说实话，真心觉得入门书和白书结构安排和讲解都有点奇怪，于是把高中的这本《Free Pascal 语言与基础算法》（真心是非常赞的一本基础算法书）拿出来重新复习一遍基础算法。寒假都去弄博客了，结果到开学第四周才弄完，简直💊。本来想边复习边总结然后分享给大家的，但是发现按照我的理解最多贴几个自己看的懂的版子就好，但是要弄到给别人看的程度内容则要几何倍的膨胀，最后就成了这个高不成低不就的四不像。因为寒假还没看 Ｃ＋＋ ，所以绝大多数内容都是由 Ｃ 完成的，导致代码显得比较臃肿。V0.0 大概就这样吧，~~如果以后用空再完善~~。另外白书和入门书没剩多少新内容了，只剩题了Orz。~~立个 flag 这学期一定要刷完!~~ 失败( ・ˍ・)

[更好阅读效果](https://www.zybuluo.com/Voleking/note/319106) 


# Basic Algorithms #


## Sort ##

STL 大法好，从此排序一行搞！  
不过各种排序代码也简单，很多方法背后的思想挺经典的，就大致打了打。没准有水题像「车厢调度」用到框架～(第一次在 CF 上做到一到类似的题还想了一下)  

+ Bubble Sort  

``` 
for (int i = 0; i < n; i++)
    for (int j = 0; j < n - i - 1; j++)
        if (a[j] > a[j + 1]) {
            int temp =  a[j];
            a[j] = a[j + 1];
            a[j + 1] = temp;
        } 
```

+ Insertion Sort  

```
for (int i = 1; i < n; i++) {
    int tmp = a[i], j;
    for (j = i - 1; j >= 0 && a[j] > tmp; j--)
        a[j + 1] = a[j];
    a[++j] = tmp; 
}
```

+ Selection Sort

```
for (int i = 0; i < n; i++)
    for (int j = i + 1; j < n; j++)
        if (a[i] > a[j]) {
            int temp = a[i];
            a[i] = a[j];
            a[j] = temp;
        }
```

+ Merge Sort

```
int mersgesort(int a[], int b[], int c[], int an, int bn) {
    int i = 0, j = 0, k = 0;
    while (i < an && j < bn) {
        if (a[i] < b[j]) {
            c[k++] = a[i++];
        }
        else {
            c[k++] = b[j++];
        }
    }
    while (i < an) 
        c[k++] = a[i++];
    while (j < bn)
        c[k++] = b[j++];
    return k;
}
```

+ Quick Sort

```   
void quicksort(int a[], int l, int r) {
    int i = l, j = r, mid = a[(l + r) / 2];
    while (i <= j) {
        while (a[i] < mid) i++;
        while (a[j] > mid) j--;
        if (i <= j) {
            int tmp = a[i];
            a[i] = a[j];
            a[j] = tmp;
            i++;
            j--;
        }
    }
    if (i < r) quicksort(a, i, r);
    if (l < j) quicksort(a, l, j);        
    return ;
}
```

+ Heap Sort  
    * 见堆的内容


### Problems ###
+ 车厢重组（冒泡排序思想，选择排序框架完成）
+ 士兵站队




## Recurrence ##

+ 棋盘格数  
n＊m 方格棋盘:   
    包含正方形个数 $\sum_{i=0}^{min(n,m)-1} (n-i)*(m-i)$  

    包含长方形个数(乘法原理，含正方形) ${\sum_{i=1}^n i}*{\sum_{i=1}^m i}$ 


### Common recurrence relations ###

1. Fibonacci
2. Hanoi
3. 平面分隔
4. Catalan
5. Stirling




## Recursion ##

主要是理解思想，几道简单的练习题：  

+ 进制转换
+ Hanoi汉诺塔 移动过程（双色汉诺塔）
+ 2 的幂次方（NOIP1998）




## DFS ##


### Module ###

```   
int dfs(int step, ...parameter list) {
    if success {
        print;
        return 0;
    }
    for (;;) 
        if satisfied {
            save condition;
            dfs(step++, ...parameter list);
            //recover precondintion;
        }
}
```



### Problems ###

+ 排列，组合，自然数拆分
+ 马的遍历，迷宫问题
+ 最佳调度，图的 m 着色问题，部落卫队




## BFS ##


### Module ###

```    
void bfs() {
    初始化，初始状态存入队列；
    队列首指针 head = 0，尾指针 tail = 1；
    while (head < tail) {
        if 当前节点为目标节点 
            输出并退出；
        for (;;) {
            if satisfied & unreached {
                存入新节点;
                tail++;
            }
        }     
        head++;
    }
}
```

相比与 DFS，BFS 常用于求最优解。  


### Problem ###

+ 最少转弯问题
+ 细胞
+ Children of the Candy Corn




## Greedy Algorithm ##

思想：局部最优推导整体最优。常需要排序等预处理。  

>大胆猜测，细心验证


### Problems ###

+ 排队打水
+ 均分纸牌
+ 删数问题
+ 拦截导弹（最大不上升＆最大上升）




## Divide And Conquer Algorithm ##


### Problems ###

+ 循环比赛日程表
+ 取余运算 （a * b % k = (a % k) * (b % k) % k）
+ 黑白棋子移动
+ 光荣的梦想（mergesort 求逆序对，Ps 车厢调度）
+ 小车问题
+ 麦森数（高精度+快速幂）  




## DP ##

在多阶段决策问题中，各阶段采取的决策，一般来说与阶段有关的，决策依赖于当前状态，又随即引起状态的转移，一个决策序列就是在变化的状态中产生出来的，故有“动态”的含义，我们称解决多阶段决策最优化过程为动态规划程序设计方法。  

基本概念于模型构成：  

1. 阶段和阶段变量  
2. 状态和状态变量  
3. 决策、决策变量和决策允许集合  
4. 策略和最优策略  
5. 状态转移方程  
 
需满足条件:

+ 最优化原则  
+ 无后效性原则  


### Knapsack Problem ###

* 0/1 背包

$$f[i, v] = max(f[i - 1, v], f[i - 1, v - w[i]] + c[i])$$

```
for (int i = 0; i < n; ++i)
    for (int v = V; v >= w[i]; v--)
        f[v] = max(f[v], f[v- w[i]] + c[i]);
```

* 完全背包

$$f[i, v] = max(f[i - 1, v], f[i - 1, v - w[i]] + c[i])$$

```
for (int i = 0; i < n; ++i)
    for (int v = w[i]; v <= V; ++v)
        f[v] = max(f[v], f[v- w[i]] + c[i]);
```

注意循环顺序的不同背后思路。  

+ 一个简单的优化：若两件物品 i、j 满足 $w[i] ≤ w[j]$ 且 $c[i] ≥ c[j]$，则讲物品 j 去掉，不用考虑。  
+ 转化为 01 背包问题求解：  
    * 第 i 种物品转化为 $\frac{V}{w[i]}$ 件费用于价值均不变的物品。  
    * 第 i 种物品拆成费用为 $w[i] * 2^k$，价值为 $c[i] * 2^k$ 的若干件物品其中 k 满足 $w[i] * 2^k < V$

* 多重背包

$$f[i, v] = max(f[i - 1, v - k * w[i]] + k * c[i] | 0 <= k <= n[i])$$

+ 优化：转化为 01 背包问题  
    * 将第 i 件物品分成若干件物品，每件物品的系数分别为：$1,2,4,\ldots,2^{(k - 1)},n[i]-2^k$
    * ** 根据 w，v 范围改变 DP 对象，可以考虑针对不同价值计算最小的重量。（ $f[i, j]$，其中 j 代表价值总和）**

```
for (int i = 0; i < N; ++i) {
    int k;
    for (k = 1 << 0; k <= n[i] && w[i] * k <= V; n[i] -= k, k <<= 1) {
        for (int v = V; v >= w[i] * k; --v) 
            f[v] = max(f[v], f[v- w[i] * k] + c[i] * k);
    }
    k = n[i];
    if ( k > 0 && w[i] * k <= V) {
        for (int v = V; v >= w[i] * k; --v) 
            f[v] = max(f[v], f[v- w[i] * k] + c[i] * k);
    }
}
```

* 混合三种背包

&emsp;&emsp;弄清楚上面三种背包后分情况就好  

* 二维费用背包

$$f[i, v, u] = max(f[i - 1, v, u], f[i - 1, v - a[i], u - b[i]] + c[i])$$

二维费用可由最多取 m 件等方式隐蔽给出。  

* 分组背包

$$f[k, v] = max(f[k - 1, v], f[k - 1, v - w[i]] + c[i] | i \in K)$$

```
    for (int k = 0; k < K; ++k)
        for (v = V; v >= 0; --v)
            for (int i = 0; i <= n[k]; ++i)
                f[v] = max(f[v], f[v - w[i]] + c[i]);
```

显然可以对每组中物品应用完全背包中“一个简单有效的优化”  

* 有依赖背包

由 NOIP2006 金明的预算方案引申，对每个附件先做一个 01 背包，再与组件得到一个 $V - w[i] + 1$ 个物品组。  
更一般问题，依赖关系由「森林」形式给出，涉及到树形 DP 以及泛化物品，这里不表。  

* 背包问题方案总数

$$f[i, v] = sum(f[i - 1, v], f[i - 1, v - w[i]] + c[i]),f[0, 0] = 0$$

>>更多内容详见「背包九讲」

## Several simple optimization method ##

1. 每次扩展只与上次状态有关，使用 **滚动数组** a[i & 1]  
2. 通过变量之间关系 **降维** （传纸条）。  
3. 做两遍避免起点遍历（能量项链）。  

## Basic DP Problem ##

+ 最长不下降子序列（拦截导弹、友好城市、合唱队形）
    * 注：可以通过二分查找将复杂度优化到 $O(NlogN)$  
+ 石子归并、乘积最大、编辑距离、方格取数、低价购买、最长公共子序列、复制书稿、橱窗布置、对抗赛、单词划分、饥饿的牛、护卫队、数字游戏、能量项链、传纸条、垃圾陷阱、守望者的逃离、矩阵取数游戏……  

### 记忆化搜索代替动规 ###

+ 滑雪  




# Data Structure #


## Stack——LIFO ##

1. Push  
2. Pop  


### Problem ###

+ 任意进制转换  
+ 括号匹配  
+ 表达式计算$\left(+ - * / ()\right)$  
+ 车厢调度  
+ 前中后缀表达式转换  




## List——FIFO ##

head：队头指针；tail：尾指针。  
优化——循环队列：  

    tail = (tail + 1) / n;  
    if (head == tail) 队列已满;  
    else Q[tail] = X;  

### Problem ###

+ 面积(换个角度看待问题)  
+ 家庭问题  

## Tree ##

+ 基本概念  
    * 结点、根、结点的度（树的度）、层次、森林、路径（对于任意两个不同的结点，如果从一个结点出发，自伤而下沿着树中连着结点的线段能到达另一结点）  
+ 树的遍历  
    1. 先序遍历  
    2. 后序遍历  
    3. 层次遍历  
    4. 叶结点遍历  

### Binary Tree ###

+ 基本概念  
    * 完全二叉树    
    * 满二叉树    
+ 二叉树遍历  
    * 先序遍历（对应前缀表示、波兰式）    
    * 中序遍历(中缀表示)  
    * 后序遍历（后缀表示、逆波兰式）  
    * 给定中序和其他一种遍历就可以确定一个二叉树  
+ 普通树转二叉树  
    * 第一个儿子左结点  
    * 兄弟右结点  
+ 树的计数问题  
    * 递归：B0 = 1， Bn = ∑BiBn-i-1  
    * Bn = C(n,2n)/(n + 1)  


### Heap ###

```
void put(int x) {
    a[++len] = x;
    int p = len;
    while (p != 1 && a[p] < a[p / 2]) {
        int tmp = a[p];
        a[p] = a[p / 2];
        a[p / 2] = tmp;
        p /= 2;
    }
    return ;
}
int get() {
    int num = a[1];
    a[1] = a[len--];
    int fa = 1, son = 0;
    while (fa * 2 <= len) {
        if (fa * 2 + 1 > len || a[fa * 2] < a[fa * 2 + 1])
            son = fa * 2;
        else
            son = fa * 2 + 1;
        if (a[fa] > a[son]) {
            int tmp = a[fa];
            a[fa] = a[son];
            a[son] = tmp;
            fa = son;
        }
        else
            break;
    }
    return num;
}
```

```
void sift(int i) {
    Data tmp = a[i];
    while (i * 2 <= len) {
        if (i * 2 + 1 > len || a[i * 2].fish > a[i * 2 + 1].fish)
            i = i * 2;
        else
            i = i * 2 + 1;
        if (tmp.fish < a[i].fish)
            a[i / 2] = a[i];
        else {
            i /= 2;
            break;
        }
    }
    a[i] = tmp;
}
// 建堆
for (int i = 1; i <= n / 2; ++i)
    hp.sift(i);
```

### Problem ###

+ 合并果子  
+ 鱼塘钓鱼  



# Graph Theory #

简单定义与概念：  

+ 边与点的集合
+ **有向图**，**无向图**，**结点的度**（**入度**、**出度**），**权值**，**连通**，**回路**（**环**），**完全图**（**稠密图**、**稀疏图**），**强连通分量**（有向图中任意两点都连通的最大子图）
+ **欧拉回路**（一笔画问题）  
+ **哈米尔顿环**（不重复走过所有路径的回路）  

图的存储与遍历：  

+ 存储
    1. 二位数组邻接矩阵存储  
    2. 数组模拟邻接表存储  
    3. 链式存储  
+ 遍历  
    1. DFS  
    2. BFS  


## Shortest Path Algorithm ##

* Floyed-Warshall——$O(N^3)$

```
init: dis[u][v] = w[u][v]() or INT_MAX / 3 //防止判断时超出整数范围
for (int k = 1; k <= n; ++k)
    for (int i = 1; i <= n; ++i)
        for (int j = 1; i <= n; ++j)
            dis[i][j] = min(dis[i][k] + dis[k][j], dis[i][j]);
```

如果规定每条边只走一次，可以求出负权回路的最短路径。修改循环顺序。

* Dijkstra  $O(N^2)$ 

算法描述（蓝白点思想）：  
设起点为 s，dis[v] 表示从 s 到 v 的最短路径，pre[v] 为 v 的前驱节点，用来输出路径。  

+ $init: dis[v] = ∞ (v ≠ s); dis[s] = 0; pre[s] = 0;$
+ $for(int\text{ }i = 1; i <= n; ++i)$
    1. 在没有被访问过的点中找一个顶点 u 使得 dis[u] 是最小的。
    2. u 标记为已确定最短路径。
    3. 更新 u 与每个未确定最短路的顶点 v 的距离
        * $dis[v] = min(dis[u] + w[u][v], dis[v])$

```
memset(vis, 0, sizeof(vis));
for (int i = 1; i <= n; ++i) {
    dis[i] = (i != s)? w[s][i] : 0;
}
for (int i = 1; i <= n; ++i) {
    double mmin = DBL_MAX / 3;
    int k = 0;
    for (int j = 1; j <= n; ++j)
        if (!vis[j] && dis[j] < mmin) {
            mmin = dis[j];
            k = j;
        }
    if (!k) break;
    vis[k] = 1;
    for (int j = 1; j <= n; ++j) {
        dis[j] = min(dis[k] + w[k][j],dis[j]);
    }
}
```

* Bellman-Ford $O(NE)$  

算法实现：  
设起点为 s，dis[v] 表示从 s 到 v 的最短路径，pre[v] 为 v 的前驱节点，用来输出路径。   

```
init: dis[v] = ∞ (v ≠ s); dis[s] = 0; pre[s] = 0;
for(int i = 1; i < N; ++i)
    for (int j = 1; j <= E; ++j)
        if (dis[u] + w[j] < dis[v]) {
            dis[v] = dis[u] + w[j];
            pre[v] = u;id
        }
```

可以处理存在负边权的情况，但无法处理存在负权回路的情况。若算法完成后，还出现某条边使得：$dis[u] + w < dis[v]$，则存在负权回路。如果一开始将 d 初始化为0，那么可以找出所有负圈。

* SPFA $O(kE)$

对 Bellman-Ford 算法的一种队列实现，减小冗余计算。  

主要思想：  
初始时将起点加入队列，每次从队列中取出一个元素，并对与它相邻的点进行修改，如果某个相邻的点修改成功，则将其入队（已经v入队的无需入队）。直到队列为空是算法结束。注意一个点可以多次入队，使用循环队列可以使队列长度只需开到 $2 * n + 5$。另外需要用邻接表储存。

```
for (int i = 1; i <= n; ++i) {
    dis[i] = (i != s)? DBL_MAX / 3 : 0;
}
memset(vis, 0, sizeof(vis));
vis[s] = true;
que.push(s);
while (!que.empty()) {
    int u = que.front();
    que.pop();
    vis[u] = false;
    for (int i = 1; i <= adj[u][0]; ++i) {
        int v = adj[u][i];
        if (dis[v] > dis[u] + w[u][v]) {
            dis[v] = dis[u] + w[u][v];
            if (!vis[v]) {
                que.push(v);
                vis[v] = true;
            }
        }
    }
}
```

### Problem ###

+ 牛的旅行  
+ 香甜的黄油  


## Connectivity of Graphs ##

* 判断是否连通   
    1. Floyed 算法  
    2. DFS 遍历  
* 最小环问题（找出一个环各边权值和最小)  
   
``` 
for (int k = 1; k <= n; ++k) {
    for (int i = 1; i < k; ++i)
        for (int j = i + 1; j < k; ++j)
            ans = min(dis[i][j] + w[i][k] + w[k][j])
    for (int i = 1; i <= n; ++i)
        for (int j = 1; j <= n; ++j)
            dis[i][j] = min(dis[i][k] + dis[k][j], dis[i][j]);
}
```

* 求有向图的强连通分量  
    
    Kosaraju 算法可以求有向图中强连通分量，描述如下：  

    1. 第一次对图 G 进行 DFS 遍历，并在遍历过程中，记录每个点退出顺序。  
    2. 倒装每一条边的方向，构造出一个反图 G'。然后按照退出顺序的逆序对对反图进行第二次 DFS 遍历，每次遍历得到的点属于一个强连通分量。

### Problem ###

有趣的一道题：刻录光盘

## Union-find set ##

```
int find(int x) {
    return (f[x] == x)? x : f[x] = find(f[x]);
};
int merge(int a, int b) {
    int fa = find(a);
    int fb = find(b);
    if (fa != fb)
    f[fa] = fb;
    // f[find(a)] = find(b);
}
```

### Problem ###

+ 格子游戏  
+ 团伙（拆点思想）  
+ 打击犯罪（逆着搞一遍）  

## Spanning tree ##

* Prime——$O(N^2)$

算法描述：  
以 1 为起点生成最小生成树，min[v] 表示蓝点 v 与白点相连的最小边权。

```
for (int i = 1; i <= n; ++i) {
    int k = 0, mmin = INT_MAX;
    for (int j = 1; j <= n; ++j)
        if (!visit[j] && dis[j] < mmin) {
            mmin = dis[j];
            k = j;
        }
    visit[k] = true;
    total += di0s[k];
    for (int j = 1; j <= n; ++j) if (!visit[j])
        dis[j] = min(g[k][j], dis[j]);
}
```

* Kruskal——$O(ElogE)$

算法描述：
按边排序，并查集维护

## Topological Sorting and Critical Path ##

用有向无环图表示一个工程中每个子工程的先后关系称为“AOV 网”，把一条有向边起点的活动称为终点活动的「前驱活动」，同理终点的活动称为起点活动的「后继活动」。只有一个活动全部的前驱全部完成之后，这个活动才能进行。

## Topological Sorting ##

算法描述：  
1. 选择一个入度为 0 的顶点并输出；
2. 然后从 AOV 网中删除此顶点及以此结点为起点的所有关联边（更新终点的入度）；
3. 重复 1，2 两步直到不存在入度为 0 的顶点为止；
4. 若输出的顶点小于网络中的顶点数，则有回路，否则输出结点序列为拓扑序列。

### Problem ###

+ 奖金

## Critical Path ##

一个工程的每项活动先后关系及所需时间通过带边权的有向无环图表示，则该网络称为“AOE 网”。为了估算某个工程的时间，需要找出影响工程完成时间的主要活动。其中源点和汇点分别表示工程的开始和结束。

算法描述：  
用拓扑排序顺序依次计算所有时间最早发生时间(其中事件 j 是事件 k 的直接前驱事件):
$$ earliest[1] = 0 $$ 
$$ earliest[k] = max(earliest[j] + dis[j][k]) $$


