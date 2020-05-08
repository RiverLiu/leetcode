# 22-括号生成

tags: 字符串，回溯算法
- https://leetcode-cn.com/problems/generate-parentheses/

使用DFS遍历 + 剪枝方法进行实现，剪枝条件：如果左/右括号已经使用完，左括号个数少于右括号数目.

```java
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> ss = new ArrayList<>();
        combineParentesis(ss, "", n, 0, 0);
        return ss;
    }

    private void combineParentesis(List<String> ss, String s, int n, int left, int right) {
        if (left > n || right > n || left < right) {
            return;
        }
        if (left == n && right == n) {
            ss.add(s);
        }
        combineParentesis(ss, s + "(", n, left + 1, right);
        combineParentesis(ss, s + ")", n, left, right + 1);
    }
}
```

```java
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> ss = new ArrayList<>();
        combineParentesis(ss, "", n, n);
        return ss;
    }

    private void combineParentesis(List<String> ss, String s, int left, int right) {
        if (left < 0 || right < 0 || left > right) {
            return;
        }
        if (left == 0 && right == 0) {
            ss.add(s);
            return;
        }
        combineParentesis(ss, s + "(", left - 1, right);
        combineParentesis(ss, s + ")", left, right - 1);
    }
}
```