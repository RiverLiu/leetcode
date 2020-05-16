# 152-乘积最大子数组

tags: 数组，动态规划
- https://leetcode-cn.com/problems/maximum-product-subarray/

解法思路: 在前 x 个子数组中，寻找最大和最大的值，如果第 x 个元素是负数，则前x的最小元素与当前元素相乘，否则最大元素与当前元素相乘，如果前面的最大或者最小值与单个值相比，选择最大或者最小的值。

```java
class Solution {
    public int maxProduct(int[] nums) {
        int max = 1, min = 1, gMax = Integer.MIN_VALUE;
        for (int num : nums) {
            if (num < 0) {
                int tmp = max;
                max = min;
                min = tmp;
            }
            max = Math.max(num * max, num);
            min = Math.min(num * min, num);

            gMax = Math.max(max, gMax);
        }
        return gMax;
    }
}
```

可额外参考：https://time.geekbang.org/course/detail/100019701-69781

python 的解法：

```py
class Solution:
    def maxProduct(self, nums: List[int]) -> int:
        if nums is None: return 0

        # 生成二维数组，第一维表示最值，第二维表示正负
        dp = [[0 for _ in range(2)] for _ in range(2)]

        # 对初始最大值，最小值，最值进行序列化
        dp[0][0], dp[0][1], res = nums[0], nums[0], nums[0]

        for i in range(1, len(nums)):
            # 二维数组，进行第一行，第二行滚动，
            # 目的为了不改写原来的值，因为下一步操作会使用原始值
            x, y = i % 2, (i - 1) % 2

            # 寻找最大值
            dp[x][0] = max(dp[y][0] * nums[i], dp[y][1] * nums[i], nums[i])
            
            # 寻找最小值
            dp[x][1] = min(dp[y][0] * nums[i], dp[y][1] * nums[i], nums[i])

            # 如果当前最大值比最终的最大值大，则进行修改
            res = max(res, dp[x][0])
        
        return res

```

