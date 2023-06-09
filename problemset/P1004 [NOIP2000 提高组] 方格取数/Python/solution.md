# 题目链接
你可以在这个链接上找到这个题目：https://www.luogu.com.cn/problem/P1004

# 题目描述
在一个 $N \times N$ 的二维方格图中，我们在其中的某些方格中填入了正整数，其他的方格中放入了数字 $0$。你需要从左上角出发，可以向下或向右行走，直到到达右下角。在走过的路上，你可以取走方格中的数。现在你需要找出两条这样的路径，使得取得的数之和为最大。要求每条路径都需要从左上角走到右下角。

# 解题思路
这是一道经典的动态规划题。我们需要找出两条路径，以便最大化我们取得的数的和。注意到我们只能向下或向右行走，这意味着任何一条从左上角到右下角的路径，都包含了恰好 $2N-2$ 步。因此，我们可以通过两个维度描述两条路径的状态：即两条路径分别已经走过的步数。如果我们设定 `dp[i][j][k]` 表示第一条路径走过 `i` 步，第二条路径走过 `j` 步，并且第二条路径当前所在的格子为 `(k,j+i-k)`，那么第一条路径所在的格子就为 `(i+j-k,k)`。

我们可以逐步进行动态规划，枚举每一步可能的行走方向，然后取所有可能行走方向中的最大值。

我们需要注意的一点是，当两条路径走到同一个格子时，我们不能重复取得同一个格子中的数。因此，在更新动态规划的状态时，我们需要判断两条路径是否到达了同一个格子。

# 代码

```python
N = int(input())
grid = [[0]*N for _ in range(N)]
while True:
    x, y, v = map(int, input().split())
    if x == y == v == 0:
        break
    grid[x-1][y-1] = v

dp = [[[0]*N for _ in range(N)] for _ in range(2*N)]
for i in range(N):
    for j in range(N):
        for k in range(max(i, j)+1):
            l = i + j - k
            if k < j:
                dp[i][j][k] = max(dp[i-1][j][k], dp[i][j-1][k])
            elif l < i:
                dp[i][j][k] = max(dp[i-1][j][k-1], dp[i][j-1][k-1])
            else:
                dp[i][j][k] = max(dp[i-1][j][k-1], dp[i][j-1][k-1], dp[i-1][j][k], dp[i][j-1][k])
            if i == j == k:
                dp[i][j][k] += grid[i][j]
            else:
                dp[i][j][k] += grid[i][j] + grid[k][l]
print(dp[N-1][N-1][N-1])
```

# 优化
上述代码已经是较优的解法，时间复杂度为 $O(N^3)$，考虑到 $N \le 9$，这是可以接受的。

# 其他方案
目前没有更好的解法，动态规划是解决这类问题的通用方法。

# 结论
通过这道题目，我们可以学习到如何使用动态规划解决问题，以及如何进行状态转移。此外，还能学习到如何在动态规划中处理特殊情况，例如本题中两条路径走到同一个格子的情况。我们还需要注意Python中的列表切片和输入输出方式。