# 79-单词搜索

tags: 数组，回溯算法
- https://leetcode-cn.com/problems/word-search/

单词搜索，使用遍历 + dfs的方法。复用了 board 数组，修改后，并还原其值。

```java
class Solution {
    public boolean exist(char[][] board, String word) {
        for (int i = 0; i < board.length; ++i) {
            for (int j = 0; j < board[0].length; ++j) {
                if (dfs(board, word, i, j, 0)) {
                    return true;
                }
            }
        }
        return false;
    }

    public boolean dfs(char[][] board, String word, int i, int j, int k) {
        if (word.length() == k) {
            return true;
        }
        if (i < 0 || i >= board.length || j < 0 || j >= board[0].length || board[i][j] != word.charAt(k)) {
            return false;
        }
        board[i][j] -= 'a';

        boolean result = dfs(board, word, i - 1, j, k + 1)
         || dfs(board, word, i + 1, j, k + 1)
         || dfs(board, word, i, j - 1, k + 1)
         || dfs(board, word, i, j + 1, k + 1);
         board[i][j] += 'a';
         return result;
    }
}
```