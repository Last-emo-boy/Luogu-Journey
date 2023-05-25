# 过河卒 - NOIP2002 普及组

## 题目链接
[洛谷P1002 过河卒](https://www.luogu.com.cn/problem/P1002)

## 题目描述
棋盘上 A 点有一个过河卒，需要走到目标 B 点。卒行走的规则：可以向下、或者向右。同时在棋盘上 C 点有一个对方的马，该马所在的点和所有跳跃一步可达的点称为对方马的控制点。现在要求你计算出卒从 A 点能够到达 B 点的路径的条数，假设马的位置是固定不动的，并不是卒走一步马走一步。

## 解题思路
这是一道典型的动态规划题目。我们可以定义一个二维数组 dp[n][m] 表示到达每个点的路径数。dp[i][j] 可以通过 dp[i-1][j] (如果存在) 和 dp[i][j-1] (如果存在) 累加得到。同时，要注意马的位置以及马可以控制的位置，这些位置的 dp 值都应设为0，因为卒不能走到这些位置。

## Java 解题代码
```java
import java.util.Scanner;

public class Main {
    private static int[] dx = {-2, -1, 1, 2, 2, 1, -1, -2, 0};
    private static int[] dy = {1, 2, 2, 1, -1, -2, -2, -1, 0};
    private static int[][] dp;
    private static boolean[][] blocked;

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        int m = scanner.nextInt();
        int hx = scanner.nextInt();
        int hy = scanner.nextInt();
        dp = new int[n+1][m+1];
        blocked = new boolean[n+1][m+1];
        for (int i = 0; i < 9; ++i) {
            int nx = hx + dx[i];
            int ny = hy + dy[i];
            if (nx >= 0 && nx <= n && ny >= 0 && ny <= m) {
                blocked[nx][ny] = true;
            }
        }
        dp[0][0] = 1;
        for (int i = 0; i <= n; ++i) {
            for (int j = 0; j <= m; ++j) {
                if (blocked[i][j]) continue;
                if (i > 0) dp[i][j] += dp[i-1][j];
                if (j > 0) dp[i][j] += dp[i][j-1];
            }
        }
        System.out.println(dp[n][m]);
    }
}
```
这段代码首先读取了输入，并初始化了dp数组和blocked数组，然后设置了马的位置和马可以控制的位置为不可到达，接着从左上角开始遍历棋盘，对每个位置计算其路径数，最后输出dp[n][m]。

## 优化
以上的 Java 解题代码已经相当优化，采用动态规划思想，在空间和时间复杂度上都是最优的。

## 其他方案
动态规划是解决这个问题的最主流和高效的方法。如果需要探索其他方法，可以尝试使用深度优先搜索（DFS）或回溯法等，但在效率上可能不如动态规划。

## 结论
通过这个问题，我们可以了解到动态规划的基本思想和应用，以及如何利用状态转移方程来解决实际问题。同时也提醒我们在解题过程中，要注意各种特殊情况，例如本题中马的位置和其控制的位置需要特别处理。