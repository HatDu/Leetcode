[剑指 Offer 39. 数组中出现次数超过一半的数字](https://leetcode-cn.com/problems/shu-zu-zhong-chu-xian-ci-shu-chao-guo-yi-ban-de-shu-zi-lcof/)

难度简单

数组中有一个数字出现的次数超过数组长度的一半，请找出这个数字。

你可以假设数组是非空的，并且给定的数组总是存在多数元素。

 

**示例 1:**

```
输入: [1, 2, 3, 2, 2, 2, 5, 4, 2]
输出: 2
```

 

**限制：**

```
1 <= 数组长度 <= 50000
```



**思路：**

使用摩尔投票法，摩尔投票法的思想是正负抵消：

- 设置数组第一个元素为候选人candidate，并将其得票数votes设置为1
- 从第二个元素开始遍历数组，记录为指针curCandidate
  - 如果curCandidate与candidate相同，则得票votes加1，否则减1
  - 判断votes是否为0，若为0则将candidate设置为curCandidate，votes重置为1

原理：如果以为candidate的得票数超过半数，那么其最终votes会大于0.



**代码：**

```java
class Solution {
    public int majorityElement(int[] nums) {
        if(nums == null || nums.length == 0) return 0;
        int n = nums.length;
        int cur = nums[0], votes=1;
        for(int i = 1; i < n; i++){
            if(nums[i] != cur) --votes;
            else ++votes;
            if(votes == 0){
                cur = nums[i];
                votes = 1;
            }
        }
        return cur;
    }
}
```

