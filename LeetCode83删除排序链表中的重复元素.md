[83.删除排序链表中的重复元素](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list/)

# 题目描述

给定一个排序链表，删除所有重复的元素，使得每个元素只出现一次。

**示例:**

```
输入: 1->1->2->3->3
输出: 1->2->3
```

# 题解

迭代

# 代码

```java
//Java
//执行用时：0ms
//内存消耗：37.9MB
//时间复杂度O(n),空间复杂度0(1)
class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        if(head == null || head.next == null){//如果链表中没有节点，或只有一个节点，直接返回
            return head;
        }
        int temp = head.val;//因为是排序链表，为了使哑结点与链表中结点不同，哑结点中存储一个特殊的数
        ListNode dummyHead = new ListNode(temp - 1);
        dummyHead.next = head;
        ListNode prev = dummyHead, curr = head;//通过curr遍历链表
        while(curr != null){
            if(prev.val == curr.val){
                prev.next = curr.next;
                curr = curr.next;
            }else{
                prev = curr;
                curr = curr.next;
            }
        }
        return dummyHead.next;
    }
}
```

递归解法如下：

```java
class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        if(head == null || head.next == null){
            return head;
        }
        ListNode nextv = deleteDuplicates(head.next);
        if(head.val == nextv.val){
            head.next = nextv.next;
        }
        return head;
    }
}
```

