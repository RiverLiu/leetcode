# 52-n皇后 ii

tags: 回溯算法
- https://leetcode-cn.com/problems/n-queens-ii/

按照51-n皇后解法，统计计数.

```java
class Solution {

    private int count = 0;

    public int totalNQueens(int n) {
        int[] queues = new int[n];
        solveNQueens(queues, 0, n);
        return count;
    }

    public void solveNQueens(int[] queens, int row, int n) {
        if (row == n) {
            ++count;
            return;
        }
        for (int col = 0; col < n; ++col) {
            if (isOk(queens, row, col)) {
                queens[row] = col;
                solveNQueens(queens, row + 1, n);
            }
        }
    }

    public boolean isOk(int[] queens, int row, int column) {
        for (int i = 0; i < row; ++i) {
            if (column == queens[i] || row - column == i - queens[i] || row + column == i + queens[i]) {
                return false;
            }
        }
        return true;
    }

}
```

采用位运算的方法。参考：https://time.geekbang.org/course/detail/100019701-67648

```
class Solution {

    private int count = 0;

    public int totalNQueens(int n) {
        dfs(n, 0, 0, 0, 0);
        return count;
    }

    public void dfs(int n, int row, int col, int pie, int na) {
        // 终止条件
        if (n == row) {
            ++count;
            return;
        }

        // col | pie | na 的位数 0 表示可用位置，1 表示不可用
        // 取反的作用是使用 1 表示可用，因为位运算方便处理 1
        // (1 << n) - 1 这个数用于将最高 32 - n 位去掉
        int bits = (~( col | pie | na)) & ((1 << n) - 1);
        while (bits > 0) {
            // 取其中位数为 1 的位置
            int p = bits & (-bits);
            // 迭代下一行，同时 col | p 列的位置不可以使用，
            // (pie | p) 在当前行时，撇的列不可以使用，向左移动1位，表示  row + 1 的撇
            // (na | p) 在当前行，捺的列不可以使用，向右移动1位，表示 row + 1 的捺
            dfs(n, row + 1, col | p, (pie | p) << 1, (na | p) >> 1);
            
            // 将最后一位1去掉，表示已经占用
            bits = bits & (bits - 1);
        }
    }

}
```
