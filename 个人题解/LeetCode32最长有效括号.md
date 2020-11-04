[32.最长有效括号](https://leetcode-cn.com/problems/longest-valid-parentheses/)

# 题目描述

给定一个只包含 `'('` 和 `')'` 的字符串，找出最长的包含有效括号的子串的长度。

**示例:**

```
输入: "(()"
输出: 2
解释: 最长有效括号子串为 "()"

输入: ")()())"
输出: 4
解释: 最长有效括号子串为 "()()"
```

# 题解一

动态规划

设置一个数组dp[n]，其中dp[i]代表以第i个字符结尾的最长有效括号的长度。dp[i]初始化为0。

对字符串从左到右进行遍历，遇到左括号"("则跳过，什么都不做；如遇到右括号，分两种情况：

第一种情况，右括号前面的一个字符是左括号，那么dp[i] = dp[i - 2] + 2（示例：")()()" )；

第二种情况，右括号前面还是右括号

2.1 dp[i-1] = 0，则dp[i] = 0（示例："))()"）

2.2 dp[i - 1] != 0，且位置i - 1 - dp[i - 1]的字符为左括号，则dp[i] = dp[i - 2 - dp[i - 1]] + dp[i - 1] + 2  （示例：")(())"）

# 代码

```java
//Java
//执行用时：1ms
//内存消耗：38.4MB
//时间复杂度O(n),空间复杂度0(n)
class Solution {
    public int longestValidParentheses(String s) {
        int n = s.length();
        int[] dp = new int[n];
        int maxLen = 0;
        //从下标为1的位置遍历可以简化判断过程
        for (int i = 1; i < n; i++) {
            //左括号则什么都不做
            if (s.charAt(i) == ')') {
                //一定要避免数组越界
                if (s.charAt(i - 1) == '(') {
                    dp[i] = (i - 2 >= 0 ? dp[i - 2] : 0) + 2;
                } else if (i - dp[i - 1] > 0 && s.charAt(i - dp[i - 1] - 1) == '(') {
                    dp[i] = dp[i - 1] + 2 + (i - dp[i - 1] - 2 >= 0 ? dp[i - dp[i - 1] - 2] : 0);
                }
                maxLen = Math.max(maxLen, dp[i]);
            }
        }
        return maxLen;
    }
}
```



# 题解二

利用栈

我们在遍历字符串的过程中判断到目前为止扫描的子串的有效性，同时能得到最长有效括号的长度。

具体做法：始终保持栈底元素为当前已经遍历过的元素中**最后一个没有被匹配的右括号的下标**，栈里其他元素维护左括号的下标：

- 对于遇到的每个"("，我们将它的下标放入栈中

- 对于遇到的每个")"，我们先弹出栈顶元素表示匹配了当前右括号：

  1.如果栈为空，说明当前右括号为没有被匹配的右括号，我们将其下标放入栈中更新最后一个没有被匹配的右括号的下标

  2.如果栈不为空，当前右括号的下标减去栈顶元素即为以**该右括号为结尾的最长有效括号的长度**

  为了保持统一，一开始需要往栈里放入一个值为-1的元素。

# 代码

```java
//Java
//执行用时：3ms
//内存消耗：38.7MB
//时间复杂度O(n),空间复杂度0(1)
class Solution {
    public int longestValidParentheses(String s) {
        int maxLen = 0;
        Stack<Integer> stack = new Stack<>();
        stack.push(-1);
        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) == '(') {
                stack.push(i);
            } else {
                stack.pop();
                if (stack.empty()) {
                    stack.push(i);
                } else {
                    maxLen = Math.max(maxLen, i - stack.peek());
                }
            }
        }
        return maxLen;
    }
}
```

