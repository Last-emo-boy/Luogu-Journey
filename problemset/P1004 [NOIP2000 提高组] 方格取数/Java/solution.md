# 题目链接
你可以在这个链接上找到这个题目：https://www.luogu.com.cn/problem/P1004

# 题目描述
在一个 $N \times N$ 的二维方格图中，我们在其中的某些方格中填入了正整数，其他的方格中放入了数字 $0$。你需要从左上角出发，可以向下或向右行走，直到到达右下角。在走过的路上，你可以取走方格中的数。现在你需要找出两条这样的路径，使得取得的数之和为最大。要求每条路径都需要从左上角走到右下角。

# 解题思路
这是一道经典的动态规划题。我们需要找出两条路径，以便最大化我们取得的数的和。注意到我们只能向下或向右行走，这意味着任何一条从左上角到右下角的路径，都包含了恰好 $2N-2$ 步。因此，我们可以通过两个维度描述两条路径的状态：即两条路径分别已经走过的步数。如果我们设定 `dp[i][j][k]` 表示第一条路径走过 `i` 步，第二条路径走过 `j` 步，并且第二条路径当前所在的格子为 `(k,j+i-k)`，那么第一条路径所在的格子就为 `(i+j-k,k)`。

我们可以逐步进行动态规划，枚举每一步可能的行走方向，然后取所有可能行走方向中的最大值。

我们需要注意的一点是，当两条路径走到同一个格子时，我们不能重复取得同一个格子中的数。因此，在更新动态规划的状态时，我们需要判断两条路径是否到达了同一个格子。

# 代码
```java
import java.util.Scanner;

public class Main {
    private static int[][] grid = new int[11][11];
    private static int[][][] dp = new int[21][11][11];
    
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int N = scanner.nextInt();
        
        while (true) {
            int x = scanner.nextInt();
            int y = scanner.nextInt();
            int v = scanner.nextInt();
            if (x == 0 && y == 0 && v == 0) {
                break;
            }
            grid[x][y] = v;
        }

        for (int t = 2; t <= 2 * N; ++t) {
            for (int i = Math.max(1, t - N); i <= Math.min(N, t - 1); ++i) {
                for (int j = Math.max(1, t - N); j <= Math.min(N, t - 1); ++j) {
                    dp[t][i][j] = Math.max(Math.max(dp[t - 1][i - 1][j - 1], dp[t - 1][i - 1][j]), Math.max(dp[t - 1][i][j - 1], dp[t - 1][i][j])) + grid[i][t - i] + grid[j][t - j];
                    if (i == j) {
                        dp[t][i][j] -= grid[i][t - i];
                    }
                }
            }
        }

        System.out.println(dp[2 * N][N][N]);
    }
}
```

# 优化
此代码已经是最优的解法。时间复杂度为 $O(N^3)$ ，对于 $N \le 9$ 的问题规模，这是可以接受的。

# 其他方案
目前没有更好的解法，动态规划是解决此类问题的通用方法。

# 结论
通过这道题目，我们学习了如何使用动态规划来处理路径选择问题，尤其是当存在多条路径时。我们需要注意的是，在更新动态规划状态时，要判断是否有多条路径经过同一个格子，并做出适当处理。