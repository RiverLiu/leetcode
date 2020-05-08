# 51-N皇后

tags: 回溯算法
- https://leetcode-cn.com/problems/n-queens/

对角线的特征： 行 - 列 是固定值，行 + 列 是固定值。

```java
class Solution {
    private byte[] dots;

    public List<List<String>> solveNQueens(int n) {
        dots = new byte[n];
        for (int i = 0; i < n; ++i) {
            dots[i] = '.';
        }

        List<List<String>> solutions = new ArrayList<>();
        int[] queues = new int[n];
        solveNQueens(solutions, queues, 0, n);
        return solutions;
    }

    public void solveNQueens(List<List<String>> solutions, int[] queens, int row, int n) {
        if (row == n) {
            List<String> locs = new ArrayList<>(n);
            for (int i = 0; i < n; ++i) {
                dots[queens[i]] = 'Q';
                locs.add(new String(dots));
                dots[queens[i]] = '.';
            }
            solutions.add(locs);
            return;
        }
        for (int col = 0; col < n; ++col) {
            if (isOk(queens, row, col)) {
                 queens[row] = col;
                solveNQueens(solutions, queens, row + 1, n);
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