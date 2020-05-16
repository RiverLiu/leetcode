# 231-2的幂

tags: 位运算，数学
- https://leetcode-cn.com/problems/power-of-two/

解法一: 整除的方法

```java
class Solution {
    public boolean isPowerOfTwo(int n) {
        if (n <= 0) {
            return false;
        }
        while (n != 1) {
            if ((n & 1) != 0) {
                return false;
            }
            n = n >> 1;
        }
        return true;
    }
}
```

解法二: 利用 2次幂的数，只有一位数为1，如果使用`n & (n - 1)` 将最低一位的1去掉，该数字将变成 0.

```java
class Solution {
    public boolean isPowerOfTwo(int n) {
        return n > 0 && (n & (n - 1)) == 0;
    }
}
```