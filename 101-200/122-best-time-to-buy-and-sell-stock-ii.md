# 122-买卖股票的最佳时机 II

tags: 数组, 贪心算法
- https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-ii/

> 贪心算法，一次遍历，只要今天价格小于明天价格就在今天买入然后明天卖出，时间复杂度 $$O(n)$$

买卖可以进行多次，同一天可以卖/买

```java
class Solution {
    public int maxProfit(int[] prices) {
        int ans = 0;
        for (int i = 1, size = prices.length; i < size; ++i) {
            if (prices[i] > prices[i - 1]) {
                ans += prices[i] - prices[i - 1];
            }
        }
        return ans;
    }
}
```

> DP动态规划，第$$i$$天只有两种状态，不持有或持有股票，当天不持有股票的状态可能来自今天卖出或者昨天也不持有，同理，当天持有股票的状态可能来自今天买入或者昨天也持有中，取最后一天的不持有股票状态就是问题的解

```java
class Solution {
    public int maxProfit(int[] prices) {
       if (prices.length <= 1) {
           return 0;
       }
       int n = prices.length;
       int dp[][] = new int[n][2];
       dp[0][0] = 0;
       dp[0][1] = -prices[0];
       // dp[i][0]表示第i天不持有股票, dp[i][1]表示第i天持有股票
       for (int i = 1; i < n; ++i) {
           dp[i][0] = Math.max(dp[i-1][0], dp[i-1][1] + prices[i]);
           dp[i][1] = Math.max(dp[i-1][1], dp[i-1][0] - prices[i]);
       }
       return dp[n - 1][0];
    }
}
```