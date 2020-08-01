#### [剑指 Offer 37. 序列化二叉树](https://leetcode-cn.com/problems/xu-lie-hua-er-cha-shu-lcof/)

难度困难53

请实现两个函数，分别用来序列化和反序列化二叉树。

**示例:** 

```
你可以将以下二叉树：

    1
   / \
  2   3
     / \
    4   5

序列化为 "[1,2,3,null,null,4,5]"
```

注意：本题与主站 297 题相同：https://leetcode-cn.com/problems/serialize-and-deserialize-binary-tree/

通过次数15,018

提交次数28,743



**思路：**

先序序列化字符串，先序反序列化。



**代码：**

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
public class Codec {
    // Encodes a tree to a single string.
    public String serialize(TreeNode root) {
        if(root == null){
            return "null,";
        }
        return String.valueOf(root.val) + "," + serialize(root.left) + serialize(root.right);
    }

    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        String[] nodes = data.split(",");
        return reDeserialize(nodes, new int[1]);
    }

    public TreeNode reDeserialize(String[] nodes, int[] i){
        if(nodes[i[0]].equals("null")){
            ++i[0];
            return null;
        }
        TreeNode node = new TreeNode(Integer.valueOf(nodes[i[0]]));
        ++i[0];
        node.left = reDeserialize(nodes, i);
        node.right = reDeserialize(nodes, i);
        return node;
    }
}

// Your Codec object will be instantiated and called as such:
// Codec codec = new Codec();
// codec.deserialize(codec.serialize(root));
```

