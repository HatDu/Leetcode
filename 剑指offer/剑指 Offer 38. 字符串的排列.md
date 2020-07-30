[剑指 Offer 38. 字符串的排列](https://leetcode-cn.com/problems/zi-fu-chuan-de-pai-lie-lcof/)

输入一个字符串，打印出该字符串中字符的所有排列。你可以以任意顺序返回这个字符串数组，但里面不能有重复元素。

示例：

```
输入：s = "abc"
输出：["abc","acb","bac","bca","cab","cba"]
```

限制：

```
1 <= s 的长度 <= 8
```



思路：

1. 使用perm函数生成数组下标全排列
2. 使用HashSet去重

代码：

```java
class Solution {
    public String[] permutation(String s) {
        String[] ans = null;
        if(s == null || s.length() < 1) return ans;
        int n = s.length();

        int[] permArr = new int[n];
        for(int i = 1; i < n; i++){
            permArr[i] = i;
        }
        List<int[]> permList = new ArrayList<>();
        // 生成全排列
        permutation(permArr, 0, n-1, permList);

        Set<String> set = new HashSet<>();
        char[] chars = s.toCharArray();
        char[] tmp = new char[chars.length];
        int[] tmpArr = null;
        for(int i = 0; i < permList.size(); i++){
            tmpArr = permList.get(i);
            for(int j = 0; j < n; j++){
                tmp[j] = chars[tmpArr[j]];
            }
            set.add(String.valueOf(tmp));
        }
        int i = -1;
        ans = new String[set.size()];
        for(String str : set){
            ans[++i] = str;
        }
        return ans;
    }

    private void permutation(int[] arr, int k, int m, List<int[]> permList){
        if(k == m){
            permList.add(Arrays.copyOf(arr, arr.length));
        }else{
            for(int i = k; i <= m; i++){
                swap(arr, k, i);
                permutation(arr, k+1, m, permList);
                swap(arr, k, i);
            }
        }
    }

    private void swap(int[] arr, int k, int m){
        int tmp = arr[k];
        arr[k] = arr[m];
        arr[m] = tmp;
    }
}
```



