#### [剑指 Offer 12. 矩阵中的路径](https://leetcode-cn.com/problems/ju-zhen-zhong-de-lu-jing-lcof/)

难度中等134

请设计一个函数，用来判断在一个矩阵中是否存在一条包含某字符串所有字符的路径。路径可以从矩阵中的任意一格开始，每一步可以在矩阵中向左、右、上、下移动一格。如果一条路径经过了矩阵的某一格，那么该路径不能再次进入该格子。例如，在下面的3×4的矩阵中包含一条字符串“bfce”的路径（路径中的字母用加粗标出）。

[["a","**b**","c","e"],
["s","**f**","**c**","s"],
["a","d","**e**","e"]]

但矩阵中不包含字符串“abfb”的路径，因为字符串的第一个字符b占据了矩阵中的第一行第二个格子之后，路径不能再次进入这个格子。

 

**示例 1：**

```
输入：board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
输出：true
```

**示例 2：**

```
输入：board = [["a","b"],["c","d"]], word = "abcd"
输出：false
```

**提示：**

- `1 <= board.length <= 200`
- `1 <= board[i].length <= 200`

注意：本题与主站 79 题相同：https://leetcode-cn.com/problems/word-search/

通过次数40,535

提交次数91,093


思路：广搜

```java
class Solution {
    private final int[][] dirs = {{0, 1}, {0, -1}, {1, 0}, {-1, 0}};
    public boolean exist(char[][] board, String word) {
        if(board.length == 0 || board[0].length == 0){
            return false;
        }
        int m = board.length, n = board[0].length;
        boolean[][] visited = new boolean[m][n];
        char[] arr = word.toCharArray();

        for(int i = 0; i < m; ++i){
            for(int j = 0; j < n; ++j){
                if(board[i][j] == arr[0]){
                    if(dfs(board, visited, arr, i, j, 1)){
                        return true;
                    }
                }
            }
        }
        return false;
    }

    private boolean dfs(char[][] board, boolean[][] visited, char[] arr, int i, int j, int cur){
        if(cur == arr.length){
            return true;
        }
        visited[i][j] = true;
        for(int[] d : dirs){
            int newx = i + d[0];
            int newy = j + d[1];
            if(newx >= 0 && newy >= 0 && newx< board.length && newy < board[0].length && board[newx][newy] == arr[cur]&& !visited[newx][newy]){

                if(dfs(board, visited, arr, newx, newy, cur + 1)){
                    return true;
                }
            }
        }
        visited[i][j] = false;
        return false;
    }
}
```