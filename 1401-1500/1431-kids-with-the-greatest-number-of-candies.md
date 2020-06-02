# 1431-拥有最多糖果的孩子

- tags: 数组
- https://leetcode-cn.com/problems/kids-with-the-greatest-number-of-candies/

过于简单，忽略该题

```java
class Solution {
    public List<Boolean> kidsWithCandies(int[] candies, int extraCandies) {
        int max = candies[0];
        for (int candy : candies) {
            max = Math.max(candy, max);
        }

        List<Boolean> res = new ArrayList<>(candies.length);
        for (int candy : candies) {
            res.add(candy + extraCandies >= max);
        }
        return res;
    }
}
```