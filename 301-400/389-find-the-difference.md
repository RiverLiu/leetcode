# 389-找不同

- tags: 位运算，哈希表
- https://leetcode-cn.com/problems/find-the-difference/

解法一: 通过求和，然后作差，算出添加的字符

```java
class Solution {
    public char findTheDifference(String s, String t) {
        char[] sc = s.toCharArray();
        char[] tc = t.toCharArray();

        int diff = 0;
        for (int i = 0; i < sc.length; i++) {
            diff += tc[i] - sc[i];
        }
        return (char)((int)tc[sc.length] + diff);
    }
}
```

解法二： 通过位运算，相同数字异或结果为0，异或与顺序无关。

```java
class Solution {
    public char findTheDifference(String s, String t) {
        int c = 0;
        int m = s.length();
        for (int i = 0; i < m; i++) {
            c ^= s.charAt(i) ^ t.charAt(i);
        }
        return (char)(c ^ t.charAt(m));
    }
}
```