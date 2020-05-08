# 563-二叉树的坡度

tags: 树
- https://leetcode-cn.com/problems/binary-tree-tilt/

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
    public int findTilt(TreeNode root) {
        if (root == null || (root.left == null && root.right == null)) {
            return 0;
        }
        int left = findTilt(root.left);
        int right = findTilt(root.right);

        if (root.left == null) {
            root.val += root.right.val;
            return left + right + Math.abs(root.right.val);
        } else if (root.right == null) {
            root.val += root.left.val;
            return left + right + Math.abs(root.left.val);
        } else {
            root.val = root.val + root.left.val + root.right.val;
            return left + right + Math.abs(root.left.val - root.right.val);
        }
    }
}
```
