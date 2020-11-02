[2.两数相加](https://leetcode-cn.com/problems/add-two-numbers/)

# 题目描述

给出两个 非空 的链表用来表示两个非负的整数。其中，它们各自的位数是按照 逆序 的方式存储的，并且它们的每个节点只能存储 一位 数字。

如果，我们将这两个数相加起来，则会返回一个新的链表来表示它们的和。

您可以假设除了数字 0 之外，这两个数都不会以 0 开头。

**示例:**

```
输入：(2 -> 4 -> 3) + (5 -> 6 -> 4)
输出：7 -> 0 -> 8
原因：342 + 465 = 807
```

# 题解

方法一：新建一个链表用来存储这两个数相加之后的值，时间复杂度*O*(max(*m*,*n*))，空间复杂度*O*(max(*m*,*n*))。

方法二：用原来两个链表中的结点充当新链表的结点，时间复杂度*O*(max(*m*,*n*))，空间复杂度*O*(1)。

# 代码

```java
//Java
//执行用时：2ms
//内存消耗：39.3MB
//时间复杂度O(max(m,n)),空间复杂度O(max(m,n))
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode dummyHead = new ListNode(0);//定义一个哑结点
        ListNode p = l1, q = l2, curr = dummyHead;//p、q分别用来遍历l1和l2，curr为新链表当前结点
        int carry = 0;//定义对应位相加后的进位
        /*算法的精髓在这里：
        循环条件为p、q有一个非null，当p或者q为null时，其用来相加的数为0，否则为结点的值
        */
        while (p != null || q != null) {
            int x = (p != null) ? p.val : 0;
            int y = (q != null) ? q.val : 0;
            int sum = x + y + carry;
            carry = sum / 10;
            curr.next = new ListNode(sum%10);//注意要新建一个结点存储值
            //下面的语句用来更新curr、p、q
            curr = curr.next;
            if(p != null) p = p.next;
            if(q != null) q = q.next;
        }
        //最后如果进位不为0，说明还需要新建一个结点存放最后的进位1
        if(carry != 0){
            curr.next = new ListNode(carry);
        }
        return dummyHead.next;
    }
}
```



```java
//Java
//执行用时：2ms
//内存消耗：39.3MB
//时间复杂度O(max(m,n)),空间复杂度O(1)
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode curr = null;
        ListNode p = l1, q = l2;
        int carry = 0;
        while (p != null || q != null) {
            int x = (p == null) ? 0 : p.val;
            int y = (q == null) ? 0 : q.val;
            int sum = x + y +carry;
            carry = sum / 10;
            curr = (p == null) ? q: p;
            curr.val = sum % 10;
            p = (p == null) ? null: p.next;
            q = (q == null) ? null: q.next;
            curr.next = (p == null)? q:p;
        }
        if(carry != 0){
            curr.next = new ListNode(1);
        }
        return l1;
    }
}
```

