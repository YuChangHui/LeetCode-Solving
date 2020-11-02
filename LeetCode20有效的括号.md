[20.有效的括号](https://leetcode-cn.com/problems/valid-parentheses/)

# 题目描述

给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串，判断字符串是否有效。

有效字符串需满足：

左括号必须用相同类型的右括号闭合。
左括号必须以正确的顺序闭合。
注意空字符串可被认为是有效字符串。

**示例:**

```
输入: "()"
输出: true

输入: "()[]{}"
输出: true

输入: "([)]"
输出: false
```

# 题解

利用栈模拟括号匹配，同时用一个映射表建立左右括号之间的联系，而不要用if-else语句判断。

# 代码

```java
//Java
//执行用时：2ms
//内存消耗：36.6MB
//时间复杂度O(n),空间复杂度0(n+m),其中m为括号字符集的大小
class Solution {
    public boolean isValid(String s) {
        int n = s.length();
        //括号数量为奇数，直接返回false
        if(n % 2 == 1){
            return false;
        }
        //用映射表存储括号匹配对，而不要用逻辑复杂的if-else语句
        Map<Character,Character> pairs = new HashMap<Character, Character>(){{
            put(')','(');
            put(']','[');
            put('}','{');
        }};
        //用栈模拟括号匹配
        Stack<Character> stack = new Stack<>();
        //对字符串s进行遍历
        for(int i = 0; i < n; i++){
            char ch = s.charAt(i);
            //if:如果是右括号，判断是否有相应左括号匹配
            //else:如果是左括号，入栈
            if(pairs.containsKey(ch)){
                if(stack.isEmpty() || stack.peek() != pairs.get(ch)){
                    return false;
                }
                stack.pop();
            }else{
                stack.push(ch);
            }
        }
        return stack.isEmpty();
    }
}
```

