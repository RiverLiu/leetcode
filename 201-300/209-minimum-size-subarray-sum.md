# 209-长度最小的子数组

- tags: 数组，双指针
- [力扣](https://leetcode-cn.com/problems/minimum-size-subarray-sum/)

>给定一个含有 n 个正整数的数组和一个正整数 s ，找出该数组中满足其和 ≥ s 的长度最小的连续子数组，并返回其长度。如果不存在符合条件的连续子数组，返回 0。

>示例: 
```
输入: s = 7, nums = [2,3,1,2,4,3]
输出: 2
解释: 子数组 [4,3] 是该条件下的长度最小的连续子数组。
```

解题思路：采用双指针的解法，控制两个指针间数字的和，如果和大于`s`，则移动左指针，再次检测和是否满足条件，满足的话，继续移动左指针，否则右指针右移。

```java
class Solution {
    public int minSubArrayLen(int s, int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }

        int first = 0;
        int second = 0;
        int sum = 0;

        // 设置初始最小长度大小
        int minLen = nums.length + 1;
        while (second < nums.length) {
            // 判断数指针相同时，数据是否满足条件
            if (first == second) {
                if (nums[first] >= s) {
                    return 1;
                } else {
                    sum += nums[first];
                    ++second;
                }
            } else {
                sum += nums[second];

                // 如果累加之和大于s，则左移左指针，判断是否满足条件
                while (sum >= s && first <= second) {
                    minLen = Math.min(minLen, second - first + 1);
                    sum -= nums[first];
                    ++first;
                }
                ++second;
            }
        }

        return minLen != nums.length + 1 ? minLen : 0;
    }
}
```

美化后的解法

```java
class Solution {
    public int minSubArrayLen(int s, int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }

        int first = 0;
        int second = 0;
        int sum = 0;
        int minLen = nums.length + 1;
        while (second < nums.length) {
            sum += nums[second];
            while (sum >= s) {
                minLen = Math.min(minLen, second - first + 1);
                sum -= nums[first];
                ++first;
            }
            ++second;
        }

        return minLen != nums.length + 1 ? minLen : 0;
    }
}

```