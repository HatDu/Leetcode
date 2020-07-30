#### [剑指 Offer 46. 把数字翻译成字符串](https://leetcode-cn.com/problems/ba-shu-zi-fan-yi-cheng-zi-fu-chuan-lcof/)

难度中等111

给定一个数字，我们按照如下规则把它翻译为字符串：0 翻译成 “a” ，1 翻译成 “b”，……，11 翻译成 “l”，……，25 翻译成 “z”。一个数字可能有多个翻译。请编程实现一个函数，用来计算一个数字有多少种不同的翻译方法。

 

**示例 1:**

```
输入: 12258
输出: 5
解释: 12258有5种不同的翻译，分别是"bccfi", "bwfi", "bczi", "mcfi"和"mzi"
```

 

**提示：**

- `0 <= num < 231`

通过次数37,550 提交次数69,663



**思路：**动态规划

首先将数字num转换成字符串str，设str长度为n，设dp[i]为前i个字符的表示方法数量0<i<n+1，则dp[i]的取值情况如下，设前一个字符与当前字符组成的十进制数字为no：

- no<10 或no>25，此时dp[i] = dp[i-1]，表示当前长度i的表示方法与长度i-1相同
- 否则，表示当前字符与前一个字符能够组成一个新的表示方法，那么dp[i] = dp[i-1] + dp[i-2]，即长度为i的表示方法为长度为i-1与i-2的表示方法之和

初始条件：dp[0]=dp[1]=1，表示还没有字符和仅有一个字符的情况时，表示方法只有一种。

**代码：**

```java
class Solution {
    public int translateNum(int num) {
        String str = String.valueOf(num);
        int n = str.length();
        int[] dp = new int[n+1];
        dp[1] = dp[0] = 1;
        char tmp = str.charAt(0);
        for(int i = 2; i <= n; i++){
            dp[i] = dp[i-1];
            char ch = str.charAt(i-1);
            int no = (tmp - '0') * 10 + ch - '0';
            if(no > 9 && no < 26){
                dp[i] += dp[i-2];
            }
            tmp = ch;
        }

        return dp[n];
    }
}
```

