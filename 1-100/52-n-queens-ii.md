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
