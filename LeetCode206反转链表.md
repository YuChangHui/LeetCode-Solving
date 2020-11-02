[206.反转链表](https://leetcode-cn.com/problems/reverse-linked-list/)

# 题目描述

反转一个单链表。

**示例:**

```
输入: 1->2->3->4->5->NULL
输出: 5->4->3->2->1->NULL
```

# 题解

可考虑使用迭代法或者递归法，递归法比较难理解。

# 代码

```java
//Java，迭代法
//执行用时：0ms
//内存消耗：38.9MB
//设置三个指针prev，curr和nextv
//时间复杂度O(n),空间复杂度0(1)
class Solution {
    public ListNode reverseList(ListNode head) {
        if(head == null) return null;
        ListNode prev = null;
        ListNode curr = head;
        //ListNode nextv = curr.next;
        while(curr != null){
            ListNode nextv = curr.next;
            curr.next = prev;
            prev = curr;
            curr = nextv;
        }
        return prev;
    }
}
```

```java
//Java，递归法
//执行用时：0ms
//内存消耗：38.5MB
//设置三个指针prev，curr和nextv
//时间复杂度O(n),空间复杂度0(n)
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

注意：做递归题目时不要陷入递归，只需要考虑递归终点、递归返回的内容是什么以及返回内容与处理位置处数据的关系。例如，在上述代码中，执行完11行代码后，整个结点关系如下：

1->2<-3<-4<-5<-last，同时2->null；head为1，head.next为2，所以需要执行12、13行代码调整head与head.next的关系