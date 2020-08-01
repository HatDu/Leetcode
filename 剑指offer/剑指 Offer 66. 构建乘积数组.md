#### [剑指 Offer 66. 构建乘积数组](https://leetcode-cn.com/problems/gou-jian-cheng-ji-shu-zu-lcof/)

难度简单31

给定一个数组 `A[0,1,…,n-1]`，请构建一个数组 `B[0,1,…,n-1]`，其中 `B` 中的元素 `B[i]=A[0]×A[1]×…×A[i-1]×A[i+1]×…×A[n-1]`。不能使用除法。

 

**示例:**

```
输入: [1,2,3,4,5]
输出: [120,60,40,30,24]
```

 

**提示：**

- 所有元素乘积之和不会溢出 32 位整数
- `a.length <= 100000`

通过次数18,453

提交次数31,609



**思路：**

设数组A与B，A[i]=a[0]\*...\*a[i]，B[i]=a[i]\*...\*a[n-1]。设结果数组为ans则有下列公式：
$$
ans[i] = A[i-1]\times B[i+1]
$$
时间复杂度
$$
O(2n)
$$
**代码：**

```java
class Solution {
    public int[] constructArr(int[] a) {
        if(a == null || a.length == 0) return new int[0];

        int n = a.length;
        int[] ans = new int[n];
        ans[0] = a[0];
        for(int i = 1; i < n; ++i){
            ans[i] = a[i] * ans[i-1];
        }

        int r = 1;
        for(int i = n -1; i > 0; --i){
            ans[i] = ans[i-1] * r;
            r *= a[i];
        }
        ans[0] = r;
        return ans;
    }
}
```