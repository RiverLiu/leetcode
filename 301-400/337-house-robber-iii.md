# 337-打家劫舍 III

tags: 树, 深度优先搜索
- https://leetcode-cn.com/problems/house-robber-iii/


采用递归方法，求解该节点时的最大值，读取偷取的节点存在两种情况：

1. 偷取该节点，则偷取孩子的孩子的左右节点
2. 不偷取该节点，则偷取左右孩子节点

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

    Map<TreeNode, Integer> moneys = new HashMap<>();

    public int rob(TreeNode root) {
        return tryRob(root);
    }

    int tryRob(TreeNode root) {
        if (root == null) {
            return 0;
        }
        if (moneys.get(root) != null) {
            return moneys.get(root);
        }

        // 偷取该节点
        int res1 = 0;
        if (root.left != null) {
            res1 = res1 + tryRob(root.left.left) + tryRob(root.left.right);
        }
        if (root.right != null) {
            res1 = res1 + tryRob(root.right.left) + tryRob(root.right.right);
        }
        res1 += root.val;

        // 不偷该节点
        int res2 = tryRob(root.left) + tryRob(root.right);
        int max = Math.max(res1, res2);
        moneys.put(root, max);
        return max;
    }
}
```