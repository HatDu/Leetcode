#### [剑指 Offer 52. 两个链表的第一个公共节点](https://leetcode-cn.com/problems/liang-ge-lian-biao-de-di-yi-ge-gong-gong-jie-dian-lcof/)



**思路：**

设链表A与链表B的公共部分长度为m，A的长度等于l1+m，B的长度为l2+m。设两个指针pa和pb，pa以l1+m+l2+m的形式遍历两个链表（即先遍历A后遍历B），pb以l2+m+l1+m的形式遍历两个链表。可以看到如果AB有公共部分，则一定会在最后的m处相遇。



**代码：**

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        ListNode pa = headA;
        ListNode pb = headB;

        while(pa != pb){
            pa = (pa == null) ? headB : pa.next;
            pb = (pb == null) ? headA : pb.next;
        }
        return pa;
    }
}
```

