# DFS简介

搜索算法：穷举问题解空间部分/所有情况，从而求出问题的解

深度优先搜索：

​	本质上是**暴力枚举**

​	深度优先：尽可能一条路走到底，走不了再回退

# DFS和n重循环

给定一个数字x，将其拆分成3个正整数，后一个要求大于等于前一个，给出方案

- 最简单的思想:三重循环暴力求解

拆分成4个正整数?
拆分成n个正整数?

- 就需要实现n重循环
- n重循环=特定的树状结构=DFS搜索

![image-20241130135528226](http://cdn.jsdelivr.net/gh/Carolynhomes/images@main/img/Python/202411301355445.png)

```python
def dfs(depth):
    """
    :params depth: 当前为第n重循环
    :return:
    """
    global cnt

    cnt += 1
    # 第0重 --- 第n-1重 都已经选好数字，此时只需要判断答案
    if depth == n:
        # 条件一：数字需要递增
        for i in range(1, n):
            if a[i] >= a[i - 1]:
                continue
            else:
                return
        # 条件二：数字和为x
        if sum(a) != x:
            return 
        # 此时是答案
        print(a)
        return 
    
    # 第depth层进行选择数字：【1，x】进行枚举
    for i in range(1, x+1):
        # 选择第depth层的数字
        a[depth] = i
        # 递归进入下一层
        dfs(depth + 1)



x, n = map(int, input().split())

# 记录每层选择数字
a = [0] * n
# 计算次数 cnt
cnt = 0

dfs(0)
print("累计计算次数={}".format(cnt))
```

## 剪枝

**把条件放在枚举的时候判断可以降低计算量**

```python
def dfs(depth, last_val):
    """
    :params depth: 当前为第n重循环
    :return:
    """
    global cnt

    cnt += 1
    # 第0重 --- 第n-1重 都已经选好数字，此时只需要判断答案
    if depth == n:
        # 条件二：数字和为x
        if sum(a) != x:
            return
        # 此时是答案
        print(a)
        return

    # 第depth层进行选择数字：【1，x】进行枚举
    # 条件一：数字需要进行递增
    for i in range(last_val, x + 1):
        # 选择第depth层的数字
        a[depth] = i
        # 递归进入下一层
        dfs(depth + 1, i)


x, n = map(int, input().split())

# 记录每层选择数字
a = [0] * n
# 计算次数 cnt
cnt = 0

dfs(0, 1)
print("累计计算次数={}".format(cnt))
```

## 模板

```python
def dfs(depth):
    """
    :param depth: 当前为第几重循环
    :return:
    """
    if depth == N:
        # N重循环最内层执行的代码
        return
    # 每重循环进行的枚举选择
```

## 例题

- 蓝桥4124

七重循环，每重循环表示1个小朋友

每个小朋友枚举所有的糖果情况

```python
ans = 0

def dfs(depth, n, m):
    """
    :param depth: 第depth个小朋友
    :param n: 第一类糖果数量
    :param m: 第二类糖果数量
    :return: 无返回值，直接修改全局变量ans
    """
    if depth == 7:
        if n == 0 and m == 0:
            global ans
            ans += 1
        return

    # 枚举第一种糖果
    for i in range(0, 6):
        # 枚举第二种糖果
        for j in range(0, 6):
            if 2 <= i + j <= 5 and i <= n and j <= m:
                dfs(depth + 1, n - i, m - j)

dfs(0, 9, 16)
print(ans)
```

- 蓝桥3505

N冲循环，每重循环三种情况

- 买1个
- 买一半
- 不买

```python
def dfs(depth, s, cnt):
    """
    :param depth: 第depth层循环
    :param s: 当前累计的重量
    :param cnt: 当前的剪的西瓜个数
    :return:
    """
    # 递归出口
    # 1、当前累计重量已经超过m，不需要继续下去
    if s > m:
        return
    # 2、当前累计重量等于m，直接更新答案
    if s == m:
        global ans
        ans = min(ans, cnt)
    # 3、第depth层时，停止继续递归
    if depth == n:
        return
    # 买一个
    dfs(depth + 1, s + w[depth], cnt)
    # 买半个
    dfs(depth + 1, s + w[depth] // 2, cnt + 1)
    # 不买
    dfs(depth + 1, s, cnt)

n, m = map(int, input().split())
m *= 2
w = list(map(int, input().split()))
w = [x * 2 for x in w]
ans = n + 1
dfs(0, 0, 0)
if ans == n + 1:
    ans = -1
print(ans)
```

# 回溯法

回溯：就是DFS的一种，在搜索尝试过程中寻找问题的解，当发现已不满足求解条件时，就“回溯”返回，尝试别的路径。

回溯更强调:此路不通，另寻他路，走过的路需要打标记

**回溯法一般在DFS的基础上加上一些剪枝策略**

## 排列树

![image-20241130144023475](http://cdn.jsdelivr.net/gh/Carolynhomes/images@main/img/Python/202411301440770.png)

## 子集树

![image-20241130144045688](http://cdn.jsdelivr.net/gh/Carolynhomes/images@main/img/Python/202411301440975.png)

# 回溯模板

## 求排列

![image-20241130144915531](http://cdn.jsdelivr.net/gh/Carolynhomes/images@main/img/Python/202411301449720.png)

排列要求数字不重复——每次选择的数字需要打标记——vis数组

要输出当前排列——记录路径——pat数组

回溯：**先打标记、记录路径、然后下一层、回到上一层、清除标记**

```python
def dfs(depth):
    # 当前为第depth个数字, 0到depth-1已经设置好
    if depth == n:
        print(path)
        return

    # 枚举第depth个数字
    for i in range(1, n + 1):
        # 数字i必须先前未选择
        if vis[i] is False:
            # 标记当前状态
            vis[i] = True
            # 记录当前路径
            path.append(i)
            # 进行下一层搜索
            dfs(depth + 1)
            # 清空标记
            vis[i] = False
            path.pop(-1)

n = int(input())
path = []
vis = [False] * (n + 1)
dfs(0)
```

## 求子集

![image-20241130145242515](http://cdn.jsdelivr.net/gh/Carolynhomes/images@main/img/Python/202411301452598.png)

```python
n = int(input())
a = list(map(int, input().split()))
path = []

def dfs(depth):
    if depth == n:
        print(path)
        return

    # 选
    path.append(a[depth])
    dfs(depth + 1)
    path.pop(-1)

    # 不选
    dfs(depth + 1)

dfs(0)
```

## 例题

- 蓝桥1508

```python
def dfs(depth):
    # 当前为第depth行数字，0到depth-1行已经设置好
    if depth == n:
        global ans
        ans = ans + 1
        return

    # 枚举第depth行放在哪列
    for i in range(1, n + 1):
        # 坐标为: (depth, i)
        # 第i列先前未选择、主对角线未选择、副对角线未选择
        if vis1[i] is False and vis2[depth + i] is False and vis3[depth - i + n] is False:
            # 标记当前状态
            vis1[i] = True
            vis2[depth + i] = True
            vis3[depth - i + n] = True
            dfs(depth + 1)
            # 清除标记
            vis1[i] = False
            vis2[depth + i] = False
            vis3[depth - i + n] = False

n = int(input())
ans = 0
vis1 = [False] * (n + 1)
vis2 = [False] * (2 * n + 1)
vis3 = [False] * (2 * n + 1)
dfs(0)
print(ans)
```

- 蓝桥182

```python
import sys
# 扩栈：递归层数过大，需要设置最大栈空间
sys.setrecursionlimit(100000)

n = int(input())
a = list(map(int, input().split()))
a = [0] + a
vis = [0] * (n + 1)

def dfs(x, length):
    # 记录当前x，已经走了length步
    vis[x] = length
    ans = 0
    for i in range(1, n + 1):
        if vis[i] == 0:
            dfs(i, 1)
    if vis[a[x]]:
        # 更新最大圈
        global ans
        ans = max(ans, length - vis[a[x]] + 1)
    # 下一步没走过，走下一步
    else:
        dfs(a[x], length + 1)

print(ans)
```

- lanqiao 178

```python
import sys
sys.setrecursionlimit(1000000)

N = int(input())
Map = []
vis = []
for i in range(N):
    Map.append(list(input()))
    vis.append([0] * N)

ans = 0
dir = [(1, 0), (0, 1), (-1, 0), (0, -1)]

# 走到(x, y)，将(x, y)所在的连通块全部标记
def dfs(x, y):
    # 标记当前点
    vis[x][y] = 1
    # 判断当前点是否为高地
    if Map[x][y + 1] == '#' and Map[x][y - 1] == '#' and Map[x + 1][y] == '#' and Map[x - 1][y] == '#':
        global flag
        flag = 1
    # 把四周的未遍历的土地继续遍历
    for i in range(4):
        xx, yy = x + dir[i][0], y + dir[i][1]
        if Map[xx][yy] == '.' and vis[xx][yy] == 0:
            dfs(xx, yy)

for i in range(N):
    for j in range(N):
        if Map[i][j] == '#' and vis[i][j] == 0:
            flag = 0
            dfs(i, j)
            if flag == 0:
                ans += 1

print(ans)
```

# 剪枝

## 例题-蓝桥

2942

![image-20241130151738774](http://cdn.jsdelivr.net/gh/Carolynhomes/images@main/img/Python/202411301517872.png)

```python
# 判断x能否加入group组
def check(x, group):
    # 要保证不能存在倍数关系
    for y in group:
        if x % y == 0 or y % x == 0:
            return False
    return True

# depth表示当前为第depth个学生
def dfs(depth):
    global ans
    # 最优性剪枝：当前已经比ans大，说明该策略不可行
    if len(Groups) > ans:
        return
    if depth == n:
        ans = min(len(Groups), ans)
        return

    for each_group in Groups:
        # 枚举第depth个学生能否加入当前组each_group
        # 前提：必须满足题意
        if check(a[depth], each_group):
            each_group.append(a[depth])
            dfs(depth + 1)
            each_group.pop()
    # 单独作为一组
    Groups.append([a[depth]])
    dfs(depth + 1)
    Groups.pop()

n = int(input())
a = list(map(int, input().split()))
# ans表示最少能分多少队
ans = n
Groups = []
dfs(0)
print(ans)
```



3075

![image-20241130151803217](http://cdn.jsdelivr.net/gh/Carolynhomes/images@main/img/Python/202411301518320.png)

```python
def dfs(depth, last_val, tot, mul):
    """
    :param depth: 第depth条边长
    :param last_val: 上一边长长度
    :param tot: 累计和
    :param mul: 累计乘积
    """
    if depth == n:
        # 前n-1条边之和大于第n条边
        if tot - path[-1] > path[-1]:
            ans[mul] += 1
        return

    for i in range(last_val + 1, 100001):
        # 最优性剪枝，后续还有n-depth个数字，每个数字都要>=i
        # 累计乘积要不超过100000: mul * (i ** (n - depth)) > 100000:
        if mul * (i ** (n - depth)) > 100000:
            break
        path.append(i)
        dfs(depth + 1, i, tot + i, mul * i)
        path.pop()

t, n = map(int, input().split())
ans = [0] * 100001
path = []
dfs(0, 0, 0, 1)

for i in range(1, 100001):
    ans[i] += ans[i - 1]
for _ in range(t):
    l, r = map(int, input().split())
    print(ans[r] - ans[l - 1])
```

# 记忆化搜索

记忆化：通过记录已经遍历过的状态的信息，从而避免对同一状态重
复遍历的搜索实现方式，
$\textcolor{red}{记忆化=dfs+额外字典}$

- 如果先前已经搜索过：直接查字典，返回字典中结果
- 如果先前没有搜索过：继续搜索，最终将该状态结果记录到字典中

## 斐波那契数列

斐波那契数列：设F[0]=1,F[1]=1,F[n]=F[n-1]+F[n-2]，求F[n]，结果对1e9+ 7取模

直接递归求解：有大量的重复计算项

记忆化搜索：**每次搜索时将当前状态答案记录到字典中**

​	后续搜索直接返回结果

![image-20241130152230782](http://cdn.jsdelivr.net/gh/Carolynhomes/images@main/img/Python/202411301522909.png)

```python
from functools import lru_cache

@lru_cache(maxsize=None)
# 这行代码将lru_cache装饰器应用于f函数。maxsize=None意味着缓存的大小没有限制，可以无限增长。这意味着函数的所有调用结果都会被缓存。
def f(x):
    if x == 0 or x == 1:
        return 1
    return f(x - 1) + f(x - 2)
```

> [!tip]
>
> 使用`lru_cache`的好处是，一旦某个`f(x)`被计算过，它的结果就会被存储在缓存中。
>
> 如果再次需要计算相同的`f(x)`，可以直接从缓存中获取结果，而不需要重新计算。
>
> 这大大减少了计算量，特别是对于大型的`x`值，因为斐波那契数列的计算会有大量的重复计算。

## 例题-lanqiao

**3820**

![image-20241130152341137](http://cdn.jsdelivr.net/gh/Carolynhomes/images@main/img/Python/202411301523240.png)

```python
from functools import lru_cache

@lru_cache(maxsize=None)
def dfs(x, y, z):
    # 当前处于(x, y)，z表示是否使用喷气背包
    # 如果能逃离，返回True，否则返回False
    if x == C - 1 and y == D - 1:
        return True

    for i in range(4):
        xx, yy = x + dir[i][0], y + dir[i][1]
        if xx < 0 or xx >= n or yy < 0 or yy >= m:
            continue
        if Map[xx][yy] < Map[x][y]:
            if dfs(xx, yy, z):
                return True
        elif Map[xx][yy] < Map[x][y] + k and z == False:
            if dfs(xx, yy, True):
                return True

    return False

# 四个方向
dir = [(1, 0), (0, 1), (-1, 0), (0, -1)]
n, m, k = map(int, input().split())
A, B, C, D = map(int, input().split())
Map = []
for i in range(n):
    Map.append(list(map(int, input().split())))

if dfs(A - 1, B - 1, False):
    print("Yes")
else:
    print("No")
```

**216**

![image-20241130152539798](http://cdn.jsdelivr.net/gh/Carolynhomes/images@main/img/Python/202411301525918.png)

```python
from functools import lru_cache

@lru_cache(maxsize=None)
def dfs(x, y, z, w):
    # 从(x, y)出发，先前已有z件宝物，已有宝物最大价值为w
    # 走到终点
    if x == n and y == m:
        # 当前不需要选择
        if z == k:
            return 1
        # 当前需要选择
        if z == k - 1:
            if w < a[x][y]:
                return 1
        # 其他情况，均为0
        return 0

    ans = 0
    # 遍历两个方向
    for delta_x, delta_y in [(1, 0), (0, 1)]:
        xx, yy = x + delta_x, y + delta_y
        if xx <= n and yy <= m:
            # 当前不选择
            ans += dfs(xx, yy, z, w)
            # 当前选择
            if w < a[x][y]:
                ans += dfs(xx, yy, z + 1, a[x][y])
    return ans % 1000000007

n, m, k = map(int, input().split())
a = [[0] * (m + 1)]
for i in range(n):
    a.append([0] + list(map(int, input().split())))
print(dfs(1, 1, 0, 0))
```

