# 213-打家劫舍 II

tags: 动态规划
- https://leetcode-cn.com/problems/house-robber-ii/submissions/

题目的意思是房屋成环，那么可以将环拆分成，偷取第一个但不偷取最后一个和不偷取第一个但可以偷取第一个，然后取两个的最大值.

```java
class Solution {
    public int rob(int[] nums) {
        int m = nums.length;
        if (m == 0) {
            return 0;
        }
        if (m == 1) {
            return nums[0];
        }
        int[] moneys = new int[m];
        moneys[0] = nums[0];
        moneys[1] = Math.max(nums[0], nums[1]);
        for (int i = 2; i < m - 1; i++) {
            moneys[i] = Math.max(moneys[i - 1], nums[i] + moneys[i - 2]);
        }
        int maxWithFirst = moneys[m - 2];

        moneys[0] = 0;
        moneys[1] = nums[1];
        for (int i = 2; i < m; i++) {
            moneys[i] = Math.max(moneys[i - 1], nums[i] + moneys[i - 2]);
        }
     
        return Math.max(maxWithFirst, moneys[m - 1]);
    }
}
```