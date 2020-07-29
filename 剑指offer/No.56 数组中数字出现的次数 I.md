[剑指 Offer 56 - I. 数组中数字出现的次数](https://leetcode-cn.com/problems/shu-zu-zhong-shu-zi-chu-xian-de-ci-shu-lcof/)

难度中等185

一个整型数组 `nums` 里除两个数字之外，其他数字都出现了两次。请写程序找出这两个只出现一次的数字。要求时间复杂度是O(n)，空间复杂度是O(1)。

 

**示例 1：**

```
输入：nums = [4,1,4,6]
输出：[1,6] 或 [6,1]
```

**示例 2：**

```
输入：nums = [1,2,10,4,1,4,3,3]
输出：[2,10] 或 [10,2]
```

 

**限制：**

- `2 <= nums.length <= 10000`

**思路1：**

使用HashMap记录每个数字出现的次数

```java
class Solution {
    public int[] singleNumbers(int[] nums) {
        Set<Integer> set = new HashSet<>();
        for(int n : nums){
            if(set.contains(n)){
                set.remove(n);
            }else{
                set.add(n);
            }
        }
        int[] ans = new int[2];
        int i = -1;
        for(int n : set){
            ans[++i] = n;
        }
        return ans;
    }
}
```



**思路2**

使用异或：

1. 一个数字与自身异或的结果为0，计算整个数组元素的异或值，将得到两个不同的数的异或值xorSum

2. 若能将两个仅出现一次的数分为两组，那么各组的异或值分别就会等于这两个仅出现一次的数

3. 如何分组？遍历对步骤1中求得的xorSum，找到数字为1的位，记录位lowBit，这说明两个仅出现一次的数字在该位上是不同的，根据此可以将数组中的元素分为两组：
   - 将元素与lowBit进行与操作，若等于0，则将其分配到当前为为0的一组，否则分配到当前位为1的一组
   - 对于仅出现一次的数字，因为本身在当前为不同，故会被分到不同的组
   - 对于其它数字，重复的数字会被分到相同的组

```java
class Solution {
    public int[] singleNumbers(int[] nums) {
        int xorSum = 0;
        for(int n : nums) xorSum ^= n;
        int lowBit = 1;

        while((xorSum&lowBit) == 0){
            lowBit <<= 1;
        }

        int[] ans = {0, 0};

        for(int n : nums){
            if((n&lowBit) == 0) ans[0] ^= n;
            else ans[1] ^= n;
        }
        return ans;
    }
}
```

