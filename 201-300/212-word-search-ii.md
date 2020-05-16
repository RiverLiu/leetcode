# 212-单词搜索 II

tags: 字典树，回溯算法
- https://leetcode-cn.com/problems/word-search-ii/

解法一： DFS + 回溯的方法，时间复杂度比较高。

```java
class Solution {
    public List<String> findWords(char[][] board, String[] words) {
        List<String> matchs = new ArrayList<>();
        for (String word : words) {
            boolean exists = false;
            for (int i = 0; !exists && i < board.length; ++i) {
                for (int j = 0; j < board[0].length; ++j) {
                    if (dfs(board, word, i, j, 0)) {
                        exists = true;
                        break;
                    }
                }
            }
            if (exists) {
                matchs.add(word);
            }
        }
        return matchs;
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