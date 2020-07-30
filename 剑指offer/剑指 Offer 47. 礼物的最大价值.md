#### [剑指 Offer 47. 礼物的最大价值](https://leetcode-cn.com/problems/li-wu-de-zui-da-jie-zhi-lcof/)

难度中等51

在一个 m*n 的棋盘的每一格都放有一个礼物，每个礼物都有一定的价值（价值大于 0）。你可以从棋盘的左上角开始拿格子里的礼物，并每次向右或者向下移动一格、直到到达棋盘的右下角。给定一个棋盘及其上面的礼物的价值，请计算你最多能拿到多少价值的礼物？

 

**示例 1:**

```
输入: 
[
  [1,3,1],
  [1,5,1],
  [4,2,1]
]
输出: 12
解释: 路径 1→3→5→2→1 可以拿到最多价值的礼物
```

 

提示：

- `0 < grid.length <= 200`
- `0 < grid[0].length <= 200`

通过次数27,070

提交次数39,674



**思路：**动态规划

设`dp[i][j]`为到达第i行，第j列多能拿到的最大礼物价值，`dp[i][j]`的递推公式如下
$$
dp[i][j] = max(dp[i-1][j], dp[i][j-1])+grid[i][j]
$$
因为`dp[i][j]`的取值仅与上一行与当前行左面的元素值有关，故可将dp数组降至一维。



**代码：**

```java
class Solution {
    public int maxValue(int[][] grid) {
        if(grid == null || grid.length < 1 || grid[0].length < 1) return 0;
        int m = grid.length, n = grid[0].length;
        int[] dp = new int[n];

        for(int i=0; i < m; ++i){
            dp[0] += grid[i][0];
            for(int j = 1; j < n; ++j){
                dp[j] = Math.max(dp[j-1], dp[j]) + grid[i][j];
            }
        }
        return dp[n-1];
    }
}
```



