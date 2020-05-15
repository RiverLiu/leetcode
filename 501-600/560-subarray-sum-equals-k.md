# 560-和为K的子数组

tags: 数组,哈希表
- https://leetcode-cn.com/problems/subarray-sum-equals-k/

题目有很多中解法。

解法一：

计算从0-i的数组累加和，然后使用 `sum[i] - sum[j] == k` 的方式，如果相等，说明[j, i] 这块子数组就是需要的数组。
时间复杂度 O(n^2)，空间复杂度 O(n)

```java
class Solution {
    public int subarraySum(int[] nums, int k) {
        int count = 0;
        int sum[] = new int[nums.length];
        for (int i = 0; i < nums.length; ++i) {
            sum[i] = i != 0 ? sum[i - 1] + nums[i] : nums[i];
            if (sum[i] == k) {
                ++count;
            }
            for (int j = 0; j < i; ++j) {
                if (sum[i] - sum[j] == k) {
                    ++count;
                }
            }
        }

        return count;
    }

}
```
优化方法，参考题解

#1: 累计和

用一个数组cumulative保存从第0个元素到当前元素的和，cumulative数组中第j个元素与第i个元素的差（cumulative[j] - cumulative[i]）即是原数组nums中第i个元素到第j个元素的和（nums[i:j]），通过两层循环计算每两个元素间的累积和。时间复杂度为$O(n^2)$，空间复杂度为$O(n)$。
```
class Solution {
public:
    int subarraySum(vector<int> &nums, int k) {
        vector<int> cul(nums.size() + 1, 0);
        int res = 0;
        for (int i = 1; i <= nums.size(); ++i)
            cul[i] = cul[i - 1] + nums[i - 1];
        for (int i = 0; i < cul.size(); ++i)
            for (int j = i + 1; j < cul.size(); ++j)
                res += cul[j] - cul[i] == k;
        return res;
    }
};
```

#2: 累计和（不使用数组）

直接通过两层循环计算两个元素间的累积和。时间复杂度为$O(n^2)$，空间复杂度为$O(1)$。

```
class Solution {
public:
    int subarraySum(vector<int> &nums, int k) {
        int size = nums.size(), res = 0;
        for (int i = 0; i < size; ++i) {
            int sum = 0;
            for (int j = i; j < size; ++j) {
                sum += nums[j];
                res += sum == k ? 1 : 0;
            }
        }
        return res;
    }
};
```

#3: 哈希表

遍历数组nums，计算从第0个元素到当前元素的和，用哈希表保存出现过的累积和sum的次数。如果sum - k在哈希表中出现过，则代表从当前下标i往前有连续的子数组的和为sum。时间复杂度为$O(n)$，空间复杂度为$O(n)$。
```
class Solution {
public:
    int subarraySum(vector<int> &nums, int k) {
        int sum = 0, res = 0;
        unordered_map<int, int> cul;
        cul[0] = 1;
        for (auto &m : nums) {
            sum += m;
            res += cul[sum - k];
            ++cul[sum];
        }
        return res;
    }
}
```