# 36-有效的数独

tags: 哈希表
- https://leetcode-cn.com/problems/valid-sudoku


第一次做的时候，以为是填写数独，这查找空间也太大了..... 查看题解，原来是题目理解错误了，是判断是否有效的数独。

使用二维数组(也可以用哈希表，数组效率更高)记录每一行每一列每一个单元格的数字是否出现，第一维表示行或者列，或者单元格的序号，记录单元格的序号有个技巧 `row / 3 * 3 + column / 3 * 3`，即从左到右，从上到下一次为0,1,...,8

```java
class Solution {
    public boolean isValidSudoku(char[][] board) {
        boolean[][] rows = new boolean[9][9];
        boolean[][] columns = new boolean[9][9];
        boolean[][] grids = new boolean[9][9];

        for (int i = 0; i < 9; ++i) {
            for (int j = 0; j < 9; ++j) {
                if (board[i][j] == '.') {
                    continue;
                }
                int val = board[i][j] - '1';
                int loc = i / 3 * 3 + j / 3;
                if (rows[i][val] || columns[j][val] || grids[loc][val]) {
                    return false;
                } else {
                    rows[i][val] = true;
                    columns[j][val] = true;
                    grids[loc][val] = true;
                }
            }
        }
        return true;
    }
}
```