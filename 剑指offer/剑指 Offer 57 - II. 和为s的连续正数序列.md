#### [剑指 Offer 57 - II. 和为s的连续正数序列](https://leetcode-cn.com/problems/he-wei-sde-lian-xu-zheng-shu-xu-lie-lcof/)

难度简单131

输入一个正整数 `target` ，输出所有和为 `target` 的连续正整数序列（至少含有两个数）。

序列内的数字由小到大排列，不同序列按照首个数字从小到大排列。

 

**示例 1：**

```
输入：target = 9
输出：[[2,3,4],[4,5]]
```

**示例 2：**

```
输入：target = 15
输出：[[1,2,3,4,5],[4,5,6],[7,8]]
```

 

**限制：**

- `1 <= target <= 10^5`

 

通过次数46,874

提交次数67,949



**思路：**

双指针法。设l=1，r=2。每次计算区间[l,r]的值，即为sum，判断是否与target相等，有三种情况：

- sum=target：找到一个区间，记录下来，l指针右移
- sum>target：当前区间和大于target，l指针右移
- sum <target：当前区间和小于target，r指针右移

递归条件：l < r < (target +1)/2

时间复杂度：
$$
O(target)=\frac{target + 1}{2}
$$
**代码：**

```java
class Solution {
    public int[][] findContinuousSequence(int target) {
        int l = 1, r = 2;
        List<List<Integer>> list = new ArrayList<>();
        int n = (target + 1) / 2;
        while(l < r && r <= target){
            int sum = (l + r)*(r - l + 1) / 2;
            if(sum == target){
                List<Integer> tmpList = new ArrayList<Integer>();
                for(int i = l; i <= r; ++i){
                    tmpList.add(i);
                }
                list.add(tmpList);
                ++l;
            }else if(sum > target){
                ++l;
            }else{
                ++r;
            }
        }

        int[][] ans = new int[list.size()][];
        for(int i = 0; i < list.size(); ++i){
            ans[i] = new int[list.get(i).size()];
            for(int j = 0; j < ans[i].length; ++j){
                ans[i][j] = list.get(i).get(j);
            }
        }
        return ans;
    }
}
```

