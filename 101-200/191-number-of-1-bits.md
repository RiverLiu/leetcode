# 191-位1的个数

tags: 位运算
- https://leetcode-cn.com/problems/number-of-1-bits/

解法一：通过比较每一位的是否为1，进行判断

```java
public class Solution {
    // you need to treat n as an unsigned value
    public int hammingWeight(int n) {
        int count = 0;
        int mask = 1;
        for (int i = 0; i < 32; ++i) {
            // 从低到高第 i 位是否为 1
            if ((n & mask) != 0) {
                ++count;
            }
            mask = mask << 1;
        }
        return count;
    }
}
```

解法二:  利用`n & (n - 1)` 将最地位的1去掉可解.

```java
public class Solution {
    // you need to treat n as an unsigned value
    public int hammingWeight(int n) {
        int count = 0;
        while (n != 0) {
            n = n & (n - 1);
            ++count;
        }
        return count;
    }
}
```