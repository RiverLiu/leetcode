# 102-二叉树的层序遍历

tags: 树, 广度优先搜索
- https://leetcode-cn.com/problems/binary-tree-level-order-traversal/

采用队列的方法进行遍历.
Notes: 队列中不可以传入 null.

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
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> vals = new ArrayList<>();
        if (root == null) {
            return vals;
        }

        Queue<TreeNode> queue = new ArrayDeque<>();
        int parent = 1, children = 0;
        queue.add(root);

        List<Integer> layer = new ArrayList(1);
        vals.add(layer);
        while (!queue.isEmpty()) {
            TreeNode node = queue.poll();
            --parent;
            layer.add(node.val);
            
            if (node.left != null) {
                queue.add(node.left);
                ++children;
            }
            if (node.right != null) {
                queue.add(node.right);
                ++children;
            }
            if (parent == 0) {
                layer = new ArrayList<>(children);
                if (children > 0) {
                     vals.add(layer);
                }
                parent = children;
                children = 0;
            } 
        }
        return vals;
    }
}
```

上面的实现未利用队列的特性，可以修改成这样.

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
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> vals = new ArrayList<>();
        if (root == null) {
            return vals;
        }

        Queue<TreeNode> queue = new LinkedList<>();
        queue.add(root);

        int count;
        List<Integer> layer;
        while (!queue.isEmpty()) {
            count = queue.size();
            layer = new ArrayList(count);
            vals.add(layer);

            while (count-- > 0) {
                TreeNode node = queue.poll();
                layer.add(node.val);
        
                if (node.left != null) {
                    queue.add(node.left);
                }
                if (node.right != null) {
                    queue.add(node.right);
                }
            }
        }
        return vals;
    }
}
```
