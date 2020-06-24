# 37-解数独

tags: 哈希表, 回溯算法

* [https://leetcode-cn.com/problems/sudoku-solver/](https://leetcode-cn.com/problems/sudoku-solver/)

采用递归和回溯的方法解决，首先标记每行，每列，每块中，数字使用的情况，然后使用深度优先的方法对数组进行遍历，在`.`的位置填写可能的数字，并修改当前数字的状态，然后，检查下一个是否可行，如果不行，进行回溯，重置之前的状态。

```java
class Solution {
    public void solveSudoku(char[][] board) {
        boolean rows[][] = new boolean[9][9];
        boolean columns[][] = new boolean[9][9];
        boolean blocks[][] = new boolean[9][9];

        for (int i = 0; i < 9; ++i) {
            for (int j = 0; j < 9; ++j) {
                if (board[i][j] != '.') {
                    int val = board[i][j] - '1';

                    rows[i][val] = true;
                    columns[j][val] = true;
                    blocks[i / 3 * 3 + j / 3][val] = true;
                }
            }
        }
        dfs(board, rows, columns, blocks, 0, 0);
    }

    private boolean dfs(char[][] board, boolean[][] rows, boolean[][] columns, boolean[][] blocks, int rowIdx, int columnIdx) {
        while (board[rowIdx][columnIdx] != '.') {
            if (columnIdx < 8) {
                ++columnIdx;
            } else if (rowIdx < 8) {
                ++rowIdx;
                columnIdx = 0;
            } else {
                return true;
            }
        }

        for (int num = 0; num < 9; ++num) {
            int blockIdx = rowIdx / 3 * 3 + columnIdx / 3;
            if (!rows[rowIdx][num]  && !columns[columnIdx][num] && !blocks[blockIdx][num]) {
                board[rowIdx][columnIdx] = (char)('1' + num);
                rows[rowIdx][num] = true;
                columns[columnIdx][num] = true;
                blocks[blockIdx][num] = true;

                if (dfs(board, rows, columns, blocks, rowIdx, columnIdx)) {
                    return true;
                } else {
                    rows[rowIdx][num] = false;
                    columns[columnIdx][num] = false;
                    blocks[blockIdx][num] = false;
                    board[rowIdx][columnIdx] = '.';
                }
            }
        }
        return false;
    }
}
```



