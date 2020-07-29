[剑指 Offer 44. 数字序列中某一位的数字](https://leetcode-cn.com/problems/shu-zi-xu-lie-zhong-mou-yi-wei-de-shu-zi-lcof/)

难度中等

数字以0123456789101112131415…的格式序列化到一个字符序列中。在这个序列中，第5位（从下标0开始计数）是5，第13位是1，第19位是4，等等。

请写一个函数，求任意第n位对应的数字。

 

**示例 1：**

```
输入：n = 3
输出：3
```

**示例 2：**

```
输入：n = 11
输出：0
```

 

**限制：**

- `0 <= n < 2^31`



**思考：**

定义如下变量：

- digit：位数，初始为1，递推digit = digit+1
- start：起始数字，初始为1，递推start = start * 10
- count：数位数量，递推start = 9\*start\*digit，即某一数位上的数字位数总和

求解分为三步：

- 确定start

  ```
  digit, start, count = 1, 1, 9
  while n > count:
      n -= count
      start *= 10 # 1, 10, 100, ...
      digit += 1  # 1,  2,  3, ...
      count = 9 * start * digit # 9, 180, 2700, ...
  ```

- 确定n所在的数字num

  ```
  num = start + (n - 1) // digit
  ```

- 根据n确定是哪一位

  ```
  s = str(num) # 转化为 string
  res = int(s[(n - 1) % digit]) # 获得 num 的 第 (n - 1) % digit 个数位，并转化为 int
  ```



**代码：**

```java
class Solution {
    public int findNthDigit(int n) {
        int digit = 1; // 数字的位数
        long start = 1; // 数字的起始大小
        long count = 9; // 当前数位上所有数字的数位长度之和
        while(n > count){
            n -= count;
            ++digit;
            start *= 10;
            count = 9*digit*start;
        }

        long num = start + (n-1) / digit;
        return Long.toString(num).charAt((n-1) % digit) - '0';
    }
}
```

