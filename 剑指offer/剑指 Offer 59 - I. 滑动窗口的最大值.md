#### [剑指 Offer 59 - I. 滑动窗口的最大值](https://leetcode-cn.com/problems/hua-dong-chuang-kou-de-zui-da-zhi-lcof/)

难度简单79

给定一个数组 `nums` 和滑动窗口的大小 `k`，请找出所有滑动窗口里的最大值。

**示例:**

```
输入: nums = [1,3,-1,-3,5,3,6,7], 和 k = 3
输出: [3,3,5,5,6,7] 
解释: 

  滑动窗口的位置                最大值
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
```

 

**提示：**

你可以假设 *k* 总是有效的，在输入数组不为空的情况下，1 ≤ k ≤ 输入数组的大小。

注意：本题与主站 239 题相同：https://leetcode-cn.com/problems/sliding-window-maximum/

通过次数32,883

提交次数74,215



**思路：**

借助[剑指 Offer 59 - II. 队列的最大值](剑指 Offer 59 - II. 队列的最大值.md)的思想，维护一个最大值队列。



**代码：**

```java
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        if(nums == null || nums.length == 0) return new int[0];
        int n = nums.length;

        Deque<Integer> dque = new LinkedList<>();
        int i = 0;
        for(; i < k; ++i){
            while(dque.size() != 0 && dque.peekLast() < nums[i]){
                dque.pollLast();
            }
            dque.offerLast(nums[i]);
        }
        int[] ans = new int [n-k+1];
        int p = -1;
        ans[++p] = dque.peekFirst();
        for(; i < n; ++i){
            if(dque.size() != 0 && dque.peekFirst().equals(nums[i - k])){
                dque.pollFirst();
            }
            while(dque.size() != 0 && dque.peekLast() < nums[i]){
                dque.pollLast();
            }
            dque.offerLast(nums[i]);
            ans[++p] = dque.peekFirst();
        }
        return ans;
    }
}
```

