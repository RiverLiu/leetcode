# 236-二叉树的最近公共祖先

tags: 树
- https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-tree

递归的思想，如果最靠前的节点是p或者q，那么公共节点就根节点，否则在左右子树中，依次访问左右子树，找到对应对应的节点就返回，最终返回到公共节点上。

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
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if (root == null || root == p || root == q) {
            return root;
        }
        TreeNode left = lowestCommonAncestor(root.left, p, q);
        TreeNode right = lowestCommonAncestor(root.right, p, q);
        if (left != null && right != null) {
            return root;
        }
        return left != null ? left, right; 
    }
}
```