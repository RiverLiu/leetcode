# 69-x 的平方根

tags: 二分查找
- https://leetcode-cn.com/problems/sqrtx

很明显的二分查找，有两个问题：临界值的判断和int溢出的问题。首位两个值的差需要大于1，int 溢出问题可以使用出发解决。

```java
class Solution {
    public int mySqrt(int x) {
        if (x == 1) {
            return 1;
        }
        int s = 0, e = x, m;
        while (e - s > 1) {
            m = (s + e) / 2;
            if (x / m < m) {
                e = m; 
            } else {
                s = m;
            }
        }

        return s;
    }
}
```