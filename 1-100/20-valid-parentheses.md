# 20-有效的括号

tags: 栈，字符串
- https://leetcode-cn.com/problems/valid-parentheses/

使用字符串的特性获取底层字节，然后新建一个数组，模拟栈使用，如果有符号的首字符，则推入栈，否则进行比较是否匹配（使用ASCII的顺序），最后比较栈的索引.

Notes: `String.getBytes()` 新生成一个数组。

```java
class Solution {
    public boolean isValid(String s) {
        byte[] symbols = s.getBytes();
        int loc = 0;

        for (byte b : symbols) {
            if (b == '(' || b == '{' || b == '[') {
                symbols[loc++] = b;
            } else {
                if (loc == 0) {
                    return false;
                }
                if (symbols[loc - 1] + 1 == b || symbols[loc - 1] + 2 == b) {
                    --loc;
                } else {
                    symbols[loc++] = b;
                }
            }
        }

        return loc == 0;
    }
}
```