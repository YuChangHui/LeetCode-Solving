[516.最长回文子序列](https://leetcode-cn.com/problems/longest-palindromic-subsequence/)

# 题目描述

给定一个字符串 `s` ，找到其中最长的回文子序列，并返回该序列的长度。可以假设 `s` 的最大长度为 `1000` 。

**示例:**

```
输入: "bbbab"
输出: 4
```

# 题解

递归方法很好理解，但是会超时。

使用动态规划，定义一个二维数组dp，dp(i,j)的含义为字符串s中从下标i到j的位置的子串中最长回文子序列的长度。dp(i,j)的大小与s(i)、s(j)是否相等有关，如果相等，则dp(i,j) = dp(i+1, j-1) + 2；如果不相等，则dp(i,j) = max( dp(i, j-1), dp(i+1, j))。遍历时需要注意遍历的顺序，i要从大向小遍历，j要从小向大遍历，这取决于dp(i,j)对于其他元素的依赖关系。

# 代码

```java
//Java
//执行用时：40ms
//内存消耗：49MB
//时间复杂度O(n^2),空间复杂度0(n^2)
class Solution {
    public int longestPalindromeSubseq(String s) {
        int n = s.length();
        //创建dp数组用于记录序列长度
        int[][] dp = new int[n][n];
        //base case
        for (int i = 0; i < n; i++) {
            dp[i][i] = 1;
        }
        //这里的遍历顺序很重要
        for (int i = n - 1; i >= 0; i--) {
            for (int j = i + 1; j < n; j++) {
                if (s.charAt(i) == s.charAt(j)) {
                    dp[i][j] = dp[i + 1][j - 1] + 2;
                } else {
                    dp[i][j] = Math.max(dp[i][j - 1], dp[i + 1][j]);
                }
            }
        }
        return dp[0][n - 1];
    }
}
```

