#### [剑指 Offer 65. 不用加减乘除做加法](https://leetcode-cn.com/problems/bu-yong-jia-jian-cheng-chu-zuo-jia-fa-lcof/)

难度简单50

写一个函数，求两个整数之和，要求在函数体内不得使用 “+”、“-”、“*”、“/” 四则运算符号。

 

**示例:**

```
输入: a = 1, b = 1
输出: 2
```

 

**提示：**

- `a`, `b` 均可能是负数或 0
- 结果不会溢出 32 位整数

通过次数16,501

提交次数29,523



**思路：**

- a^b可以得到无进位的和
- (a&b)<<1可以得到进位

则sum = (a^b) + (a&b)<<1



**代码：**

```java
class Solution {
    public int add(int a, int b) {
        while(b != 0){
            int tmp = (a&b) << 1;
            a ^= b;
            b = tmp;
        }
        return a;
    }
}
```

