# 121-买卖股票的最佳时机

tags: 数组, 动态规划
- https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock/

使用动态规划的思想实现.

1. 前 n 天的最大收益 = max(前 n-1 天的最大收益，今天的价格 - 前 n - 1 天的最低价格）

>记录【今天之前买入的最小值】
>计算【今天之前最小值买入，今天卖出的获利】，也即【今天卖出的最大获利】
>比较【每天的最大获利】，取最大值即可

```java
class Solution {
    public int maxProfit(int[] prices) {
        if (prices.length <= 1) {
            return 0;
        }
        int min = prices[0], max = 0;
        for (int i = 1; i < prices.length; ++i) {
            max = Math.max(max, prices[i] - min);
            min = Math.min(min, prices[i]);
        }
        return max;
    }
}
```