# 198-打家劫舍

tags: 动态规划
- https://leetcode-cn.com/problems/house-robber/

198. 打家劫舍

```
class Solution {
    public int rob(int[] nums) {
        if (nums.length <= 0) {
            return 0;
        }
        return dfs(nums, 0, 0);
    }

    public int dfs(int[] nums, int before, int loc) {
        if (loc >= nums.length) {
            return before; 
        }
        return Math.max(dfs(nums, before + nums[loc], loc + 2), dfs(nums, before, loc + 1));
    }
}
```

深度优先遍历，结果超时，因为存在很多重复项，可以考虑记录重复计算的值。

动态规划的方法

```
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
        for (int i = 2; i < m; i++) {
            moneys[i] = Math.max(moneys[i - 1], nums[i] + moneys[i - 2]);
        }
        return moneys[m - 1];
    }
}
```