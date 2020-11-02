[67.二进制求和](https://leetcode-cn.com/problems/add-binary/)

# 题目描述

给你两个二进制字符串，返回它们的和（用二进制表示）。

输入为 **非空** 字符串且只包含数字 `1` 和 `0`。

**示例:**

```
输入: a = "11", b = "1"
输出: "100"

输入: a = "1010", b = "1011"
输出: "10101"
```

# 题解

思路：

与十进制整数求和类似，从低位到高位依次求和。

不同点在于，此题要将求和结果存放在一个StringBuilder对象中，最后将这个对象反转以后转换为字符串输出。

# 代码

```java
//Java
//执行用时：2ms
//内存消耗：37.3MB
//时间复杂度O(max(m,n)),空间复杂度0(max(m,n))
class Solution {
    public String addBinary(String a, String b) {
        int len1 = a.length(), len2 = b.length();
        //idx1和idx2用于从后往前遍历字符串a和b
        int idx1 = len1 - 1, idx2 = len2 - 1;
        //add为进位
        int add = 0;
        //result用来记录相加后字符串的结果，与正确结果顺序相反
        StringBuilder result = new StringBuilder();
        while (idx1 != -1 || idx2 != -1) {
            int x = (idx1 == -1) ? 0 : a.charAt(idx1) - '0';
            int y = (idx2 == -1) ? 0 : b.charAt(idx2) - '0';
            int temp = x + y + add;
            result.append(temp % 2);
            add = temp / 2;
            idx1 = (idx1 == -1) ? -1 : idx1 - 1;
            idx2 = (idx2 == -1) ? -1 : idx2 - 1;
        }
        if(add != 0){
            result.append(add);
        }
        return result.reverse().toString();
    }
}
```

