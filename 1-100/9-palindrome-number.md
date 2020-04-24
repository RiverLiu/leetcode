# 回文数

tags: Simple, Math

- [题目链接](https://leetcode.com/problems/palindrome-number/)
- [领扣链接](https://leetcode-cn.com/problems/palindrome-number/)

判断是否是回文数

```java
class Solution {
    public boolean isPalindrome(int x) {
        if (x < 0) {
            return false;
        }

        int t = x;
        int y = 0;
        while (t != 0) {
            y = y * 10 + t % 10;
            t /= 10;
        }

        return x == y;
    }
}
```
