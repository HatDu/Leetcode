剑指 Offer 16. 数值的整数次方

实现函数double Power(double base, int exponent)，求base的exponent次方。不得使用库函数，同时不需要考虑大数问题。

 

示例 1:

输入: 2.00000, 10
输出: 1024.00000
示例 2:

输入: 2.10000, 3
输出: 9.26100
示例 3:

输入: 2.00000, -2
输出: 0.25000
解释: 2-2 = 1/22 = 1/4 = 0.25
 

说明:

-100.0 < x < 100.0
n 是 32 位有符号整数，其数值范围是 [−231, 231 − 1] 。
注意：本题与主站 50 题相同：https://leetcode-cn.com/problems/powx-n/

通过次数39,195提交次数118,865


思路：快速幂

代码：

```java
class Solution {
    public double myPow(double x, int n) {
        if(x == 0){
            return 0;
        }
        double p = x;
        double ans = 1.0;
        long b = n;
        if(n < 0){
            b = -b;
            p =  1 / p;
        }

        while(b > 0){
            if((b & 1) == 1){
                ans *= p;
            }
            p *= p;
            b >>= 1;
        }
        return ans;
    }
}
```
