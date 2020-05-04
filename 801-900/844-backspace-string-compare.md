# 844-比较含退格的字符串

tags: 栈, 双指针

https://leetcode-cn.com/problems/backspace-string-compare/


通过字符串通过数组实现的方法，获取字符串的数组，然后按照规则控制数组位置，并转换成字符串比较(可优化该项)。

```java
class Solution {
    public boolean backspaceCompare(String S, String T) {
        String s = parseBackSpace(S);
        String t = parseBackSpace(T);
        return s.equals(t);
    }

    public String parseBackSpace(String s) {
        byte[] bs = s.getBytes();

        int loc = 0;
        for (int i = 0, size = bs.length; i < size; ++i) {
            if (bs[i] == '#') {
                loc = Math.max(loc - 1, 0);
            } else {
                bs[loc++] = bs[i];
            }
        }
        return new String(bs, 0, loc);
    }
}
```