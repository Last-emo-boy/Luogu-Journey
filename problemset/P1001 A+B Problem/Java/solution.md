# A+B Problem - P1001

## 题目链接

[A+B Problem - P1001](https://www.luogu.com.cn/problem/P1001)

## 题目描述

输入两个整数 `a` 和 `b`，输出它们的和（|a|, |b| ≤ 10^9）。

## 解题思路

这个题目非常简单，只需要接收两个整数输入，然后将它们相加并打印出结果即可。

Java语言中，我们可以使用 `Scanner` 类从控制台读取输入。首先我们需要创建一个 `Scanner` 对象，然后使用它的 `nextInt()` 方法来读取整数。这个方法会阻塞程序的执行，直到用户输入了一个整数并按下了回车键。

读取了两个整数后，我们只需要将它们相加，并使用 `System.out.println()` 方法打印出结果即可。这个方法会自动在打印的结果后面添加一个换行符。

## 代码

以下是使用Java解决这个问题的代码：

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int a = scanner.nextInt();
        int b = scanner.nextInt();
        System.out.println(a + b);
    }
}
```

## 结论

这个题目是一个非常基础的输入/输出和整数运算问题，主要目的是帮助你熟悉Java的输入/输出和基本运算。通过这个题目，我们可以学习到以下几点：

1. 如何在Java中从控制台读取输入。
2. 如何在Java中打印输出。
3. 如何在Java中进行整数运算。

虽然这个题目很简单，但是掌握了这些基础知识，你就可以开始解决更复杂的问题了。