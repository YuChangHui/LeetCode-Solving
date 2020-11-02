[28.实现strStr()](https://leetcode-cn.com/problems/implement-strstr/)

# 题目描述

给定一个 haystack 字符串和一个 needle 字符串，在 haystack 字符串中找出 needle 字符串出现的第一个位置 (从0开始)。如果不存在，则返回  -1。

当 needle 是空字符串时，我们应当返回什么值呢？这是一个在面试中很好的问题。

对于本题而言，当 needle 是空字符串时我们应当返回 0 。这与C语言的 strstr() 以及 Java的 indexOf() 定义相符。

```
输入: haystack = "hello", needle = "ll"
输出: 2
```

# 题解

暴力匹配

# 代码

```java
//Java
//执行用时：3ms
//内存消耗：36.7MB
//时间复杂度O(mn),空间复杂度0(1)
class Solution {
    public int strStr(String haystack, String needle) {
        if (needle == null) {
            return 0;
        }
        for (int i = 0; i <= haystack.length() - needle.length(); i++) {
            int j = 0, tempI = i;
            while(tempI < haystack.length() && j < needle.length() && haystack.charAt(tempI) == needle.charAt(j)){
                tempI++;
                j++;
            }
            if(j == needle.length()){
                return i;
            }
        }
        return -1;
    }
}
```

