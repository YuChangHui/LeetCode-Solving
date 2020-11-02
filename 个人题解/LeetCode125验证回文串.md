[125.验证回文串](https://leetcode-cn.com/problems/valid-palindrome/)

# 题目描述

给定一个字符串，验证它是否是回文串，只考虑字母和数字字符，可以忽略字母的大小写。

**说明：**本题中，我们将空字符串定义为有效的回文串。

**示例:**

```
输入: "A man, a plan, a canal: Panama"
输出: true
```

# 题解一

主要利用Java的库函数

1.定义一个filter方法，作用是过滤字符串中的字符，使得符合要求的留下，返回到str1中。

2.定义一个reverse方法，作用是将一个String反转，返回一个新的String。

3.比较str1与str2的内容是否相同。

# 代码

```java
//Java，迭代法
//执行用时：7ms
//内存消耗：38.6MB
//时间复杂度O(n),空间复杂度0(n)
class Solution {
    public boolean isPalindrome(String s) {
        String str1 = filter(s);
        String str2 = reverse(str1);
        return str1.equals(str2);
    }

    public String filter(String s){//过滤无效字符
        StringBuilder stringBuilder = new StringBuilder();
        for(int i = 0; i < s.length(); i++){
            char ch = s.charAt(i);
            if(Character.isLetterOrDigit(ch)){
                stringBuilder.append(ch);
            }
        }
        return stringBuilder.toString().toUpperCase();
    }

    public String reverse(String s){//用于反转字符串
        StringBuilder stringBuilder = new StringBuilder(s);
        return stringBuilder.reverse().toString().toUpperCase();
    }
}
```



# 题解二

双指针法，直接在原字符串上进行判断即可；也可以将有效字符放在一个新的字符串中，对新字符串进行判断。

# 代码

```java
//Java，双指针法
//执行用时：3ms
//内存消耗：38.2MB
//时间复杂度O(n),空间复杂度0(1)
class Solution {
    public boolean isPalindrome(String s) {
        int left = 0, right = s.length() - 1;//初始化左右指针
        while(left < right){
            //当左指针所指字符不是数字或者字母时，更新左指针
            while(left < right && !Character.isLetterOrDigit(s.charAt(left))) left++;
            //当右指针所指字符不是数字或者字母时，更新右指针
            while(left < right && !Character.isLetterOrDigit(s.charAt(right))) right--;
            //比较这一轮符合条件的左右指针所指字符
            if(Character.toLowerCase(s.charAt(left)) != Character.toLowerCase(s.charAt(right))){
                return false;
            }
            //更新左右指针
            left++;
            right--;
        }
        return true;
    }
}
```

