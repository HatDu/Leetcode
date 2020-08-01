#### [剑指 Offer 49. 丑数](https://leetcode-cn.com/problems/chou-shu-lcof/)

难度中等54

我们把只包含质因子 2、3 和 5 的数称作丑数（Ugly Number）。求按从小到大的顺序的第 n 个丑数。

 

**示例:**

```
输入: n = 10
输出: 12
解释: 1, 2, 3, 4, 5, 6, 8, 9, 10, 12 是前 10 个丑数。
```

**说明:** 

1. `1` 是丑数。
2. `n` **不超过**1690。





**思路：**

设`dp[i]`表示第(i+1)个丑数的值，dp[0]=1，维护三个指针a、b、c，初始值a=b=c=0，那么下一个丑数的值应该是min(a\*2, b\*3, c\*5)，如果是通过下标a计算得来的下一个丑数，则a指针右移，b、c同理。



**代码：**

```java
class Solution {
    public int nthUglyNumber(int n) {
        int a = 0, b = 0, c = 0;
        int[] dp = new int [n];

        dp[0] = 1;
        for(int i = 1; i < n; ++i){
            int n1 = dp[a]*2, n2 = dp[b]*3, n3 = dp[c]*5;
            dp[i] = Math.min(n1, Math.min(n2, n3));

            if(dp[i] == n1) ++a;
            if(dp[i] == n2) ++b;
            if(dp[i] == n3) ++c;
        }
        return dp[n-1];
    }
}
```

