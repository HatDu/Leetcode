剑指 Offer 13. 机器人的运动范围
地上有一个m行n列的方格，从坐标 [0,0] 到坐标 [m-1,n-1] 。一个机器人从坐标 [0, 0] 的格子开始移动，它每次可以向左、右、上、下移动一格（不能移动到方格外），也不能进入行坐标和列坐标的数位之和大于k的格子。例如，当k为18时，机器人能够进入方格 [35, 37] ，因为3+5+3+7=18。但它不能进入方格 [35, 38]，因为3+5+3+8=19。请问该机器人能够到达多少个格子？

 

示例 1：

输入：m = 2, n = 3, k = 1
输出：3
示例 2：

输入：m = 3, n = 1, k = 0
输出：1
提示：

1 <= n,m <= 100
0 <= k <= 20
通过次数63,435提交次数126,404


思路：广度优先搜索

时间复杂度：$O(mn)$

空间复杂度：$O(mn)$

```java
class Solution {
    private final int[][] dirs = {{1, 0}, {-1, 0}, {0, 1}, {0, -1}};
    public int movingCount(int m, int n, int k) {
        boolean[][] visited = new boolean[m][n];
        Queue<int[]> queue = new LinkedList();

        queue.offer(new int[]{0, 0});
        visited[0][0] = true;
        int count = 0;
        int[] h;
        while(!queue.isEmpty()){
            h = queue.poll();
            ++count;

            for(int[] d : dirs){
                int i = h[0] + d[0];
                int j = h[1] + d[1];
                if(i >= 0 && j >= 0 && i < m && j < n && !visited[i][j]){
                    visited[i][j] = true;
                    if(getBitSum(i) + getBitSum(j) <= k){
                        queue.offer(new int[]{i, j});
                    }
                }
                
            }
        }
        return count;
    }

    private int getBitSum(int n){
        int sum = 0;
        while(n > 0){
            sum += n % 10;
            n /= 10;
        }
        return sum;
    }
}
```