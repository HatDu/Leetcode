#### [剑指 Offer 07. 重建二叉树](https://leetcode-cn.com/problems/zhong-jian-er-cha-shu-lcof/)

难度中等167

输入某二叉树的前序遍历和中序遍历的结果，请重建该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。

 

例如，给出

```
前序遍历 preorder = [3,9,20,15,7]
中序遍历 inorder = [9,3,15,20,7]
```

返回如下的二叉树：

```
    3
   / \
  9  20
    /  \
   15   7
```

 

**限制：**

```
0 <= 节点个数 <= 5000
```

 

**注意**：本题与主站 105 题重复：https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/

通过次数49,509

提交次数71,990

代码：

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    private Map<Integer, Integer> dict = new HashMap<>();
    private int[] preorder;
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        this.preorder = preorder;
        for(int i = 0; i < inorder.length; i++)
            dict.put(inorder[i], i);
        return buildTree(0, 0, inorder.length - 1);
    }

    public TreeNode buildTree(int pre_root, int in_left, int in_right){
        if(in_left > in_right) return null;
        TreeNode node = new TreeNode(preorder[pre_root]);
        int i = dict.get(preorder[pre_root]);
        node.left = buildTree(pre_root + 1, in_left, i - 1);
        node.right = buildTree(pre_root + 1 + i - in_left, i + 1, in_right);
        return node;
    }
}
```

时间复杂度：$O(n)$

空间复杂度：$O(n+h)$，n为map的大小，h为递归栈的深度。