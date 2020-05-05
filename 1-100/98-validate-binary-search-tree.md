# 98-验证二叉搜索树

tags: 树, 深度优先搜索
- https://leetcode-cn.com/problems/validate-binary-search-tree/

采用中序遍历的方法，遍历时，保存最大值.

非递归版本.

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
    public boolean isValidBST(TreeNode root) {
        Stack<TreeNode> stack = new Stack();

        // 有临界值问题，也可以使用 Long 替换
        Integer maxVal = null;
        while (!stack.isEmpty() || root != null) {
            if (root != null) {
                stack.push(root);
                root = root.left;
            } else {
                root = stack.pop();
                if (maxVal != null && root.val <= maxVal) {
                    return false;
                } else {
                    maxVal = root.val;
                }
                root = root.right;
            }
        }
        return true;
    }
}
```

递归版本.

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

    private long maxVal = Long.MIN_VALUE;

    public boolean isValidBST(TreeNode root) {
        if (root == null) {
            return true;
        }
        if (isValidBST(root.left)) {
            if (root.val <= maxVal) {
                return false;
            }
            maxVal = root.val;
            return isValidBST(root.right);
        }
        return false;
    }
}
```

递归遍历，比较整个子树的方法，通过传递子树的最大值和最小值，进行判断.

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

    public boolean isValidBST(TreeNode root) {
        return isValid(root, Long.MIN_VALUE, Long.MAX_VALUE);
    }

    private boolean isValid(TreeNode root, long min, long max) {
        if (root == null) {
            return true;
        }
        if (root.val <= min || root.val >= max) {
            return false;
        }
        return isValid(root.left, min, root.val) && isValid(root.right, root.val, max);
    }
}
```

