[92.反转链表Ⅱ](https://leetcode-cn.com/problems/reverse-linked-list-ii/)

# 题目描述

反转从位置 *m* 到 *n* 的链表。请使用一趟扫描完成反转。

**说明:**
1 ≤ *m* ≤ *n* ≤ 链表长度。

**示例:**

```
输入: 1->2->3->4->5->NULL, m = 2, n = 4
输出: 1->4->3->2->5->NULL
```

# 题解一

迭代法：首先找到需要反转序列的前一个结点，记为guard，反转序列的第一个结点，记为point，然后每次讲point后面的结点删除，并将被删除的结点插入到guard后面。

# 代码

```java
//Java
//执行用时：0ms
//内存消耗：35.8MB
//时间复杂度O(n),空间复杂度O(1)
class Solution {
    public ListNode reverseBetween(ListNode head, int m, int n) {
        ListNode dummyHead = new ListNode(-1);//定义哑结点，方便进行处理
        dummyHead.next = head;//将哑结点与原链表连接起来
        ListNode curr = dummyHead;
        int step = 0;
        while (step < m - 1) {//通过循环找到guard与point
            curr = curr.next;
            step++;
        }
        ListNode guard = curr, point = curr.next;
        curr = curr.next;
        for (int i = 0; i < n - m; i++) {//通过循环将point后需要反转的结点一个个插入到guard后面
            ListNode delNode = curr.next;
            curr.next = delNode.next;
            delNode.next = guard.next;
            guard.next = delNode;
        }
        return dummyHead.next;//返回哑结点后的第一个结点
    }
}
```

# 题解二

迭代法

首先看如何反转整个链表

```java
class Solution {
    public ListNode reverseList(ListNode head) {
        if(head == null || head.next == null){
            return head;//当头结点为null或者只有一个结点，直接返回head
        }
        ListNode last = reverseList(head.next);//不满足递归结束条件时，对后面的链表进行递归求解，返回last
        head.next.next = head;//head与head.next的关系
        head.next = null;
        return last;
    }
}
```

接着看如何反转链表前n个结点：

```java
ListNode successor = null; // 后驱节点

// 反转以 head 为起点的 n 个节点，返回新的头结点
ListNode reverseN(ListNode head, int n) {
    if (n == 1) { 
        // 记录第 n + 1 个节点
        successor = head.next;
        return head;
    }
    // 以 head.next 为起点，需要反转前 n - 1 个节点
    ListNode last = reverseN(head.next, n - 1);

    head.next.next = head;
    // 让反转之后的 head 节点和后面的节点连起来
    head.next = successor;
    return last;
}  
```

最后便可以用reverseN来实现reverseBetween了

# 代码

```java
//Java
//执行用时：0ms
//内存消耗：36.1MB
//时间复杂度O(n),空间复杂度O(n)
class Solution {
    ListNode reverseBetween(ListNode head, int m, int n) {
        // base case
        if (m == 1) {
            return reverseN(head, n);
        }
        // 前进到反转的起点触发 base case
        head.next = reverseBetween(head.next, m - 1, n - 1);
        return head;
    }
    ListNode successor = null; // 后驱节点

    // 反转以 head 为起点的 n 个节点，返回新的头结点
    ListNode reverseN(ListNode head, int n) {
        if (n == 1) {
            // 记录第 n + 1 个节点
            successor = head.next;
            return head;
        }
        // 以 head.next 为起点，需要反转前 n - 1 个节点
        ListNode last = reverseN(head.next, n - 1);

        head.next.next = head;
        // 让反转之后的 head 节点和后面的节点连起来
        head.next = successor;
        return last;
    }
}
```

