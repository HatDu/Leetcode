剑指 Offer 14- I. 剪绳子

>给你一根长度为 n 的绳子，请把绳子剪成整数长度的 m 段（m、n都是整数，n>1并且m>1），每段绳子的长度记为 k[0],k[1]...k[m-1] 。请问 k[0]*k[1]*...*k[m-1] 可能的最大乘积是多少？例如，当绳子的长度是8时，我们把它剪成长度分别为2、3、3的三段，此时得到的最大乘积是18。

示例 1：

输入: 2
输出: 1
解释: 2 = 1 + 1, 1 × 1 = 1
示例 2:

输入: 10
输出: 36
解释: 10 = 3 + 3 + 4, 3 × 3 × 4 = 36
提示：

2 <= n <= 58
注意：本题与主站 343 题相同：https://leetcode-cn.com/problems/integer-break/

通过次数50,587提交次数91,757

**思路：**

动态规划

设$dp[i]$为绳子长度为i时的最优方案，$dp[i]$有如下递推公式：
$$
dp[i] = max\{ j*(i-j), j*dp[i-j]\}, \quad 0 \leq  j \leq i
$$

表示江城子分为两段，第一段取长度为j，第二段长度为i- j。第二段可以继续划分，也可以不分。求最优的情况，则遍历i，求每次划分的最优值。


代码：

```java
class Solution {
    public int cuttingRope(int n) {
        
        int[] dp = new int[n+1];
        dp[2] = 1;

        for(int i = 3; i <= n; i++){
            int res = 0;
            for(int j = 0; j < i; j++){
                res = Math.max(res, Math.max(j*(i-j), j*dp[i-j]));
            }
            dp[i] = res;
        }
        return dp[n];
    }
}
```
