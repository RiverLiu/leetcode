# 70-爬楼梯

tags: 动态规划
- https://leetcode-cn.com/problems/climbing-stairs/

解法：这题有点类似斐波那契问题，DP方程为第 i 位置的走法时第 i - 1 位和第 i - 2 位的走法之和。

解法中，保留了前两步的值，没有使用数组保留所有的值。

```java
class Solution {
    public int climbStairs(int n) {
        if (n <= 2) {
            return n;
        }
        int step = 0, before = 1, before2 = 2;
        for (int i = 3; i <= n; ++i) {
            step = before + before2;
            before = before2;
            before2 = step;
        }
        return step;
    }
}
```