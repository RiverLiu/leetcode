# 242-有效的字母异位词

tags: 排序, 哈希表
- https://leetcode-cn.com/problems/valid-anagram/


通过hash的方法去实现，也可以通过排序的方法去实现，另外对于 ASCII 的字符，可以通过`c - 'a'` 进行索引比较。

```java
class Solution {
    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) {
            return false;
        }
        Map<Character, Integer> map = new HashMap<>();
        for (char c : s.toCharArray()) {
            map.compute(c, (k, v) -> (v == null) ? 1 : v + 1);
        }
        for (char c : t.toCharArray()) {
            Integer v = map.get(c);
            if (v == null) {
                return false;
            }
            if (v == 1) {
                map.remove(c);
            } else {
                map.put(c, v - 1);
            }
        }
        return map.isEmpty();
    }
}
```