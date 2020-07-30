#### [剑指 Offer 45. 把数组排成最小的数](https://leetcode-cn.com/problems/ba-shu-zu-pai-cheng-zui-xiao-de-shu-lcof/)

难度中等72

输入一个非负整数数组，把数组里所有数字拼接起来排成一个数，打印能拼接出的所有数字中最小的一个。

 

**示例 1:**

```
输入: [10,2]
输出: "102"
```

**示例 2:**

```
输入: [3,30,34,5,9]
输出: "3033459"
```

 

**提示:**

- `0 < nums.length <= 100`

**说明:**

- 输出结果可能非常大，所以你需要返回一个字符串而不是整数
- 拼接起来的数字可能会有前导 0，最后结果不需要去掉前导 0

通过次数22,723

提交次数40,630



**思路：**字符串比较

对于两个数字x与y，总希望最高位比较小的放在前面，将二者转成字符串，可以实现该比较

- str(x) + str(y) > str(y) + str(x)，则y应该排在x之前
- str(x) + str(y) < str(y) + str(x) ，则x应该排在y之前

**代码：**

```java
class Solution {
    public String minNumber(int[] nums) {
        int n = nums.length;
        String[] strs = new String[n];
        for(int i = 0; i < n; ++i){
            strs[i] = String.valueOf(nums[i]);
        }

        Arrays.sort(strs, (x, y) -> {return (x+y).compareTo(y+x);});

        StringBuilder sb = new StringBuilder();
        for(String str : strs){
            sb.append(str);
        }
        return sb.toString();
    }
}
```

