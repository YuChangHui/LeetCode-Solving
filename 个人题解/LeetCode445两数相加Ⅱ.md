[445.两数相加Ⅱ](https://leetcode-cn.com/problems/add-two-numbers-ii/)

# 题目描述

给你两个 非空 链表来代表两个非负整数。数字最高位位于链表开始位置。它们的每个节点只存储一位数字。将这两数相加会返回一个新的链表。

你可以假设除了数字 0 之外，这两个数字都不会以零开头。

**进阶：**

如果输入链表不能修改该如何处理？换句话说，你不能对列表中的节点进行翻转。

**示例:**

```
输入：(7 -> 2 -> 4 -> 3) + (5 -> 6 -> 4)
输出：7 -> 8 -> 0 -> 7
```

# 题解一

最简洁朴素的思想如下：由于两个整数的加法运算是从低位到高位进行的，而题目中链表是从高位开始存储数字的，因此可以先将两个链表反转，使其链表头存储最低位数字，这里我们可以定义一个方法reverseList()完成链表反转；接着我们定义另一个方法addTwoLists()完成两个数字相加的运算。注意，这时得到的链表结点中数字的顺序与正确结果中链表结点数字顺序相反，因此还需要反转一次链表得到正确结果，代码如下。

# 代码

```java
//Java
//执行用时：3ms
//内存消耗：38.1MB
//时间复杂度O(max(m,n)),空间复杂度O(m+n)
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        l1 = reverseList(l1);
        l2 = reverseList(l2);
        ListNode head = addTwoLists(l1, l2);
        head = reverseList(head);
        return head;
    }

    //定义一个反转链表的方法
    public ListNode reverseList(ListNode head) {
        if (head == null) return head;
        ListNode prev = null;
        ListNode curr = head;
        while (curr != null) {
            ListNode nextv = curr.next;
            curr.next = prev;
            prev = curr;
            curr = nextv;
        }
        return prev;
    }

    //定义一个将两个链表中数字相加的方法（此时的链表从低位到高位存储一个数字）
    public ListNode addTwoLists(ListNode l1, ListNode l2) {
        ListNode dummyHead = new ListNode(0);
        ListNode curr = dummyHead;
        ListNode p = l1, q = l2;
        int carry = 0;
        while (p != null || q != null) {
            int x = (p != null) ? p.val : 0;
            int y = (q != null) ? q.val : 0;
            curr.next = new ListNode((x + y + carry) % 10);
            curr = curr.next;
            carry = (x + y + carry) / 10;
            if (p != null) p = p.next;
            if (q != null) q = q.next;
        }
        if (carry != 0) {
            curr.next = new ListNode(carry);
        }
        return dummyHead.next;
    }
}
```

# 题解二

链表是从高位到低位存储数字的，但数字的加法需要从低位向高位进行，由于这是一个逆序的过程，因此我们可以很自然地想到用栈来解决这个问题。

# 代码

```java
//Java
//执行用时：6ms
//内存消耗：38.7MB
//时间复杂度O(max(m,n)),空间复杂度O(m+n)
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        Stack<Integer> stack1 = new Stack<>();
        Stack<Integer> stack2 = new Stack<>();
        while(l1 != null){
            stack1.push(l1.val);
            l1 = l1.next;
        }
        while(l2 != null){
            stack2.push(l2.val);
            l2 = l2.next;
        }
        int carry = 0;
        ListNode head = null;
        while(!stack1.isEmpty() || !stack2.isEmpty() || carry > 0){
            int x = stack1.isEmpty()?0:stack1.pop();
            int y = stack2.isEmpty()?0:stack2.pop();
            int sum = x + y + carry;
            ListNode node = new ListNode(sum % 10);
            node.next = head;
            head = node;
            carry = sum / 10;
        }
        return head;
    }
}
```

