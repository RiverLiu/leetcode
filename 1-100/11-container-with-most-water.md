# 盛最多水的容器

tags: Medium, Array, Two Pointer

- [题目链接](https://leetcode.com/problems/container-with-most-water/)
- [领扣链接](https://leetcode-cn.com/problems/container-with-most-water/)

```java
class Solution {
    public int maxArea(int[] height) {
        int max = 0;
        for (int i = 0; i < height.length - 1; ++i) {
            for (int j = i + 1; j < height.length; ++j) {
                max = Math.max(max, (j - i) * Math.min(height[j], height[i]));
            }
        }

        return max;
    }
}
```
