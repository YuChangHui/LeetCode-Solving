[86.分隔链表](https://leetcode-cn.com/problems/partition-list/)

# 题目描述

给定一个链表和一个特定值 *x*，对链表进行分隔，使得所有小于 *x* 的节点都在大于或等于 *x* 的节点之前。

你应当保留两个分区中每个节点的初始相对位置。

**示例:**

```
输入: head = 1->4->3->2->5->2, x = 3
输出: 1->2->2->4->3->5
```

# 题解一

新建两个链表，一个存放所有小于x的节点，另外一个存放所有大于或者等于x的节点，最后再合并两个链表。

# 代码

```java
//Java
//执行用时：0ms
//内存消耗：37.6MB
//时间复杂度O(n),空间复杂度O(n)
class Solution {
    public ListNode partition(ListNode head, int x) {
        ListNode lessHead = new ListNode(0), moreHead = new ListNode(0);//分别为新建的两个链表的哑结点
        ListNode lessCurr = lessHead, moreCurr = moreHead;
        ListNode curr = head;//用来遍历原链表的变量
        while(curr != null){
            int temp = curr.val;
            if(temp <x){
                lessCurr.next = new ListNode(temp);
                lessCurr = lessCurr.next;
            }else{
                moreCurr.next = new ListNode(temp);
                moreCurr = moreCurr.next;
            }
            curr = curr.next;
        }
        lessCurr.next = moreHead.next;
        return lessHead.next;
    }
}
```

# 题解二

优化题解一中的空间复杂度，使其降为O(1)。思路是不创建新节点（只创建两个哑结点），通过改变原来链表的结构使其符合要求。

# 代码

```java
//Java
//执行用时：0ms
//内存消耗：36.1MB
//时间复杂度O(n),空间复杂度O(1)
class Solution {
    public ListNode partition(ListNode head, int x) {
        ListNode lessHead = new ListNode(0), moreHead = new ListNode(0);
        ListNode lessCurr = lessHead, moreCurr = moreHead;
        ListNode curr = head;
        while(curr != null){
            int temp = curr.val;
            if(temp <x){
                lessCurr.next = curr;
                lessCurr = curr;
            }else{
                moreCurr.next = curr;
                moreCurr = curr;
            }
            curr = curr.next;
        }
        lessCurr.next = moreHead.next;
        moreCurr.next = null;//这条语句在此解法中必须有，因为如果不设置的话，链表中可能存在环，而上一种解法则不需要这条语句，因为节点都是新创建的，默认指向null
        return lessHead.next;
    }
}
```

