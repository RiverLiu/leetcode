# 338-比特位计数

tags: 位运算，动态规划
- https://leetcode-cn.com/problems/counting-bits/

解法一：第 x 位的数字，是数字 `(x & (x - 1))`(该数字比 `x` 小，且与`x`的区别是，最低位少了一个1) 比特计数 + 1，  

```java
class Solution {
    public int[] countBits(int num) {
        int res[] = new int[num + 1];
        for (int i = 1; i <= num; ++i) {
            res[i++] = 1 + res[i & (i - 1)];
        }
        return res;
    }
}
```