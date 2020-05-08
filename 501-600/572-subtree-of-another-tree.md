# 572-另一个树的子树

tags: 树
- https://leetcode-cn.com/problems/subtree-of-another-tree/comments/

按照深度优先遍历，添加参数 depth，表示两个树对比的深度，当depth=0时，为对比的起点，如果遇到不相等的时候，回溯到起点，从左子树或者右子树进行继续比较.
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public boolean isSubtree(TreeNode s, TreeNode t) {
        return isSubtree(s, t, 0);
    }
    public boolean isSubtree(TreeNode s, TreeNode t, int depth) {
        if (s == null && t == null) {
            return true;
        } else if (s == null || t == null) {
            return false;
        }

        if (s.val == t.val 
            && isSubtree(s.left, t.left, depth + 1)
            && isSubtree(s.right, t.right, depth + 1)) {
                return true;
        }

        if (depth == 0) {
            return isSubtree(s.left, t, 0) || isSubtree(s.right, t, 0); 
        }
    
        return false;
    }
}
```

通过对比子树，如果t是s的子树，需要满足这些条件：

- s, t是一样的
- s的左子树与t相同
- s的右子树与t相同

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public boolean isSubtree(TreeNode s, TreeNode t) {
        if (s == null) {
            return false;
        }
        return isSame(s, t) || isSubtree(s.left, t) || isSubtree(s.right, t);
    }
    public boolean isSame(TreeNode s, TreeNode t) {
        if (s == null && t == null) {
            return true;
        } else if (s == null || t == null) {
            return false;
        }

        if (s.val == t.val) {
            return isSame(s.left, t.left) && isSame(s.right, t.right);
        }
    
        return false;
    }
}
```