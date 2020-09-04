剑指 Offer 06. 从尾到头打印链表
输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。

 

示例 1：

输入：head = [1,3,2]
输出：[2,3,1]
 

限制：

0 <= 链表长度 <= 10000

通过次数85,831提交次数113,198

思路1：用数组存储

```java
class Solution {
    public int[] reversePrint(ListNode head) {
        List<Integer> list = new ArrayList<>();
        ListNode p = head;
        while(p != null){
            list.add(p.val);
            p = p.next;
        }
        int[] ans = new int[list.size()];
        int j = -1;
        for(int i = list.size() - 1; i >= 0; --i){
            ans[++j] = list.get(i);
        }
        return ans;
    }
}
```

时间复杂度：$O(n)$

空间复杂度：$O(n)$
