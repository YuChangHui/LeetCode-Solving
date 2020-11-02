[328.奇偶链表](https://leetcode-cn.com/problems/odd-even-linked-list/)

# 题目描述

给定一个单链表，把所有的奇数节点和偶数节点分别排在一起。请注意，这里的奇数节点和偶数节点指的是节点编号的奇偶性，而不是节点的值的奇偶性。

请尝试使用原地算法完成。你的算法的空间复杂度应为 O(1)，时间复杂度应为 O(nodes)，nodes 为节点总数。

**示例:**

```
输入: 1->2->3->4->5->NULL
输出: 1->3->5->2->4->NULL
```

# 题解

当然，我们可以新建立两个链表（不妨记为oddLink与evenLink），oddLink存放奇数结点的值，evenLink存放偶数结点的值，但这样的话，我们需要额外开辟n个结点空间，不满足题目对于空间复杂度的要求，因此不可以新建立链表，而是通过改变指针的指向将原来的链表分为两个链表oddLink与evenLink，最后将oddLink末尾结点的next设置为evenLink的头结点，并返回oddLink的头结点。

# 代码

```java
//Java
//执行用时：0ms
//内存消耗：38.6MB
//时间复杂度O(n),空间复杂度0(1)
class Solution {
    public ListNode oddEvenList(ListNode head) {
        if(head == null){//特殊情况判断
            return null;
        }
        //head记录oddLink头结点，oddTail记录oddLink末尾节点
        //evenHead记录evenLink头结点，evenTail记录evenLink末尾节点
        ListNode oddTail = head, evenHead = head.next, evenTail = evenHead;
        //注意循环继续条件，可根据结点个数为奇偶两种情况写出此条件
        while(evenTail != null && evenTail.next != null){
            //更新oddTail与evenTail
            oddTail.next = evenTail.next;
            oddTail = evenTail.next;
            evenTail.next = oddTail.next;
            evenTail = oddTail.next;
        }
        //将oddLink末尾结点的next设置为evenLink的头结点
        oddTail.next = evenHead;
        return head;
    }
}
```

