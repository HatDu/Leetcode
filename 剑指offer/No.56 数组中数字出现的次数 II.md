[剑指 Offer 56 - II. 数组中数字出现的次数 II](https://leetcode-cn.com/problems/shu-zu-zhong-shu-zi-chu-xian-de-ci-shu-ii-lcof/)

难度中等51

在一个数组 `nums` 中除一个数字只出现一次之外，其他数字都出现了三次。请找出那个只出现一次的数字。

 

**示例 1：**

```
输入：nums = [3,4,3,3]
输出：4
```

**示例 2：**

```
输入：nums = [9,1,7,9,7,9,7]
输出：1
```

 

**限制：**

- `1 <= nums.length <= 10000`
- `1 <= nums[i] < 2^31`



**思路1：**

使用HashMap记录每个数字出现的次数

**代码：**

```java
class Solution {
    public int singleNumber(int[] nums) {
        Map<Integer, Integer> map = new HashMap<>();
        for(int n : nums){
            Integer val = map.get(n);
            if(val == null){
                map.put(n, 1);
            }else{
                map.put(n, val + 1);
            }
        }

        for(int k : map.keySet()){
            if(map.get(k).equals(1)) return k;
        }
        return -1;
    }
}
```

