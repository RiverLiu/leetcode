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

解法二，使用Trie树的方法去遍历，首先将单词放入到Trie树中，然后开始遍历board数组，记录当前走过的路径，如果当前路径上的单词在Trie树startswith中，则继续遍历，如果是单词，则符合要求添加。

copy from:  https://leetcode.com/problems/word-search-ii/discuss/59780/Java-15ms-Easiest-Solution-(100.00)

Intuitively, start from every cell and try to build a word in the dictionary. `Backtracking (dfs)` is the powerful way to exhaust every possible ways. Apparently, we need to do `pruning` when current character is not in any word.

1. How do we instantly know the current character is invalid? `HashMap`?
2. How do we instantly know what's the next valid character? `LinkedList`?
3. But the next character can be chosen from a list of characters. `"Mutil-LinkedList"`?

Combing them, `Trie` is the natural choice. Notice that:

1. `TrieNode` is all we need. `search` and `startsWith` are useless.
2. No need to store character at TrieNode. `c.next[i] != null` is enough.
3. Never use `c1 + c2 + c3`. Use `StringBuilder`.
4. No need to use `O(n^2)` extra space `visited[m][n]`.
5. No need to use `StringBuilder`. Storing `word` itself at leaf node is enough.
6. No need to use `HashSet` to de-duplicate. Use "one time search" trie.

For more explanations, check out [dietpepsi's blog](http://algobox.org/word-search-ii/).

## Code Optimization

UPDATE: Thanks to @dietpepsi we further improved from 17ms to 15ms.

1. 59ms: Use `search` and `startsWith` in Trie class like this popular solution.
2. 33ms: Remove Trie class which unnecessarily starts from `root` in every `dfs` call.
3. 30ms: Use `w.toCharArray()` instead of `w.charAt(i)`.
4. 22ms: Use `StringBuilder` instead of `c1 + c2 + c3`.
5. 20ms: Remove `StringBuilder` completely by storing word instead of boolean in TrieNode.
6. 20ms: Remove visited[m][n] completely by modifying board[i][j] = '#' directly.
7. 18ms: check validity, e.g., `if(i > 0) dfs(...)`, before going to the next dfs.
8. 17ms: De-duplicate `c - a` with one variable i.
9. 15ms: Remove `HashSet` completely. dietpepsi's idea is awesome.

The final run time is 15ms. Hope it helps!

```java
public List<String> findWords(char[][] board, String[] words) {
    List<String> res = new ArrayList<>();
    TrieNode root = buildTrie(words);
    for (int i = 0; i < board.length; i++) {
        for (int j = 0; j < board[0].length; j++) {
            dfs (board, i, j, root, res);
        }
    }
    return res;
}

public void dfs(char[][] board, int i, int j, TrieNode p, List<String> res) {
    char c = board[i][j];
    if (c == '#' || p.next[c - 'a'] == null) return;
    p = p.next[c - 'a'];
    if (p.word != null) {   // found one
        res.add(p.word);
        p.word = null;     // de-duplicate
    }

    board[i][j] = '#';
    if (i > 0) dfs(board, i - 1, j ,p, res); 
    if (j > 0) dfs(board, i, j - 1, p, res);
    if (i < board.length - 1) dfs(board, i + 1, j, p, res); 
    if (j < board[0].length - 1) dfs(board, i, j + 1, p, res); 
    board[i][j] = c;
}

public TrieNode buildTrie(String[] words) {
    TrieNode root = new TrieNode();
    for (String w : words) {
        TrieNode p = root;
        for (char c : w.toCharArray()) {
            int i = c - 'a';
            if (p.next[i] == null) p.next[i] = new TrieNode();
            p = p.next[i];
       }
       p.word = w;
    }
    return root;
}

class TrieNode {
    TrieNode[] next = new TrieNode[26];
    String word;
}
```

