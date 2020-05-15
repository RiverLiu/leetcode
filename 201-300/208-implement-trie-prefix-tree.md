# 208-实现 Trie (前缀树)

tags: 设计，字典树
- https://leetcode-cn.com/problems/implement-trie-prefix-tree/

```java
class Trie {

    class Tree {
        boolean word;
        Tree[] next;
    }
    
    private Tree tree;

    /** Initialize your data structure here. */
    public Trie() {
        tree = new Tree();
    }
    
    /** Inserts a word into the trie. */
    public void insert(String word) {
        Tree root = tree;
        for (char c : word.toCharArray()) {
            if (root.next == null) {
                root.next = new Tree[26];
            }
         
            if (root.next[c - 'a'] == null) {
                root.next[c - 'a'] = new Tree();
            }
            root = root.next[c - 'a'];
        }
        root.word = true;
    }
    
    /** Returns if the word is in the trie. */
    public boolean search(String word) {
        Tree root = tree;
        for (char c : word.toCharArray()) {
            if (root.next == null) {
                return false;
            }
            root = root.next[c - 'a'];
            if (root == null) {
                return false;
            }
        }
        return root.word;
    }
    
    /** Returns if there is any word in the trie that starts with the given prefix. */
    public boolean startsWith(String prefix) {
        Tree root = tree;
        for (char c : prefix.toCharArray()) {
            if (root == null || root.next == null) {
                return false;
            }
            root = root.next[c - 'a'];
        }
        return root != null;
    }
}

/**
 * Your Trie object will be instantiated and called as such:
 * Trie obj = new Trie();
 * obj.insert(word);
 * boolean param_2 = obj.search(word);
 * boolean param_3 = obj.startsWith(prefix);
 */
```