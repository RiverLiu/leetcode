# 111-二叉树的最小深度

tags: 树，深度优先搜索，广度优先搜索
- https://leetcode-cn.com/problems/minimum-depth-of-binary-tree/

通过广度优先搜索遍历，如果遇到不存在左右子树，则跳出，深度即为当前的深度.

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
    public int minDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }

        Queue<TreeNode> queue = new LinkedList<>();
        queue.add(root);

        TreeNode node;
        int depth = 0, count;
        while (!queue.isEmpty()) {
            depth++;
            count = queue.size();
            while (count-- > 0) {
                node = queue.poll();
                if (node.left == null && node.right == null) {
                    return depth;
                }
                if (node.left != null) {
                    queue.add(node.left);
                }
                if (node.right != null) {
                    queue.add(node.right);
                }
            }
        }
        return depth;
    }
}
```

深度优先的遍历

```java
class Solution {
    public int minDepth(TreeNode root) {
        
        if (root == null)
            return 0;
        
        if (root.left == null && root.right != null)
            return minDepth(root.right) + 1;
        
        if (root.right == null && root.left != null)
            return minDepth(root.left) + 1;
        
        
        return Math.min(minDepth(root.left), minDepth(root.right)) + 1;

    }
}
```