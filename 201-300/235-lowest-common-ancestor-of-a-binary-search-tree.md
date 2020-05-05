# 235-二叉搜索树的最近公共祖先

tags: 树
- https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-search-tree/


利用二叉搜索树，左子树小于根节点的值，右子树大于根节点的值，公共的节点要么是这个节点中的一个，要么一个在左子树，一个在右子树上。

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

    TreeNode common = null;
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
         if ((root.val - p.val) * (root.val - q.val) <= 0) {
            return root;
        } else if (root.val < p.val && root.val < q.val) {
            return lowestCommonAncestor(root.right, p, q);
        } else {
            return lowestCommonAncestor(root.left, p, q);
        }
    }

}
```
