#### [剑指 Offer 63. 股票的最大利润](https://leetcode-cn.com/problems/gu-piao-de-zui-da-li-run-lcof/)

难度中等44

假设把某股票的价格按照时间先后顺序存储在数组中，请问买卖该股票一次可能获得的最大利润是多少？

 

**示例 1:**

```
输入: [7,1,5,3,6,4]
输出: 5
解释: 在第 2 天（股票价格 = 1）的时候买入，在第 5 天（股票价格 = 6）的时候卖出，最大利润 = 6-1 = 5 。
     注意利润不能是 7-1 = 6, 因为卖出价格需要大于买入价格。
```

**示例 2:**

```
输入: [7,6,4,3,1]
输出: 0
解释: 在这种情况下, 没有交易完成, 所以最大利润为 0。
```

 

**限制：**

```
0 <= 数组长度 <= 10^5
```



**思路1：**暴力法

双重for循环遍历所有可能的组合，算法复杂度
$$
O(n^2)
$$
**思路2：**动态规划

记dp[i]为第i天时能获取的最大利润，即min为截至到第i天为止股票的最小价格。则会有下列递推公式
$$
dp[i] = max{dp[i-1], prices[i]-min}, 0<i<n
$$
初始条件：dp[0] = 0，仅有一天，无法交易

则最终条件：dp[n-1]

因为仅需要记录前一天的最大获利，因此可用一个数字profit代替dp数组，将空间复杂度降到`O(1)`。



**代码：**

```java
class Solution {
    public int maxProfit(int[] prices) {
        if(prices == null || prices.length < 2){
            return 0;
        }
        int n = prices.length;

        int profit = 0;
        int min = prices[0];
        for(int i = 1; i < n; i++){
            profit = Math.max(profit, prices[i] - min);
            min = Math.min(min, prices[i]);
        }
        return profit;
    }
}
```

