[剑指 Offer 43. 1～n整数中1出现的次数](https://leetcode-cn.com/problems/1nzheng-shu-zhong-1chu-xian-de-ci-shu-lcof/)

难度中等

输入一个整数 `n` ，求1～n这n个整数的十进制表示中1出现的次数。

例如，输入12，1～12这些整数中包含1 的数字有1、10、11和12，1一共出现了5次。

 

**示例 1：**

```
输入：n = 12
输出：5
```

**示例 2：**

```
输入：n = 13
输出：6
```



**限制：**

- `1 <= n < 2^31`



**思路：**

将一个数拆分成四个部分：

- digit：位因子，如20的位因子为10
- cur：当前位上的数字
- high：高位数字
- low：低位数字

一个数字可以表示为：num = high*(digit+1) + cur\*digit + low



某个数位上1的个数和上面四个数有关

1. 当cur=0时，即当前位为0，当前位上的数字仅和高位有关，计算公式：high*digit

   ![](assets\No.43.1.png)

2. 当cur=1时，当前位上1的次数与高位和低位都有关，计算公式：high*digit + low + 1

   ![](assets\No.43.2.png)

3. 当1<cur<10时，1出现的次数仅由high决定，计算公式：(high+1)*digit

   ![](assets\No.43.3.png)



**代码实现：**

```java
class Solution {
    public int countDigitOne(int n) {
        int ans = 0;
        int low = 0;
        int high = n / 10;
        int cur = n % 10;
        int digit = 1;
        while(high != 0 || cur != 0){
            if(cur == 0){
                ans += high * digit;
            }
            else if(cur == 1){
                ans += high*digit + low + 1;
            }else{
                ans += (high + 1) * digit;
            }
            
            low += cur*digit;
            cur = high % 10;
            high /= 10;
            digit *= 10;
        }
        return ans;
    }
}
```

