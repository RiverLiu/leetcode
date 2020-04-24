# 整数反转

tags: Medium, String, Math

- [题目链接](https://leetcode.com/problems/string-to-integer-atoi/)
- [领扣链接](https://leetcode-cn.com/problems/string-to-integer-atoi/)

将字符串转化为正数.

```java
class Solution {
    public int myAtoi(String str) {
        if (str == null || str.length() == 0) {
            return 0;
        }

        int tmp;
        int num = 0;
        boolean flag = true;
        boolean start = false;

        for (char c : str.toCharArray()) {
            if (c == ' ') {
                if (!start) {
                    continue;
                } else {
                    break;
                }
            }
            if (c == '+') {
                if (!start) {
                    start = true;
                    continue;
                } else {
                    break;
                }
            }
            if (c == '-') {
                if (!start) {
                    flag = false;
                    start = true;
                    continue;
                } else {
                    break;
                }
            }
            if (c >= '0' && c <= '9') {
                start = true;
                tmp = num * 10 + (int)(c - '0');
                if (tmp / 10 != num) {
                    return flag ? Integer.MAX_VALUE : Integer.MIN_VALUE;
                }
                num = tmp;
            } else {
                break;
            }
        }

        return flag ? num: -num;
    }
}
```
