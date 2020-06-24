# 16-最接近的三数之和

- tags: 数组，双指针
- 题目链接: https://leetcode-cn.com/problems/3sum-closest/

求解三个数的和和目标值`target` 最接近. 采用暴力的方法，如下所示。时间复杂度为 `O(n^3)`，执行有超时的问题。

```java
class Solution {
    public int threeSumClosest(int[] nums, int target) {
        Arrays.sort(nums);
        int closetNum = nums[0] + nums[1] + nums[2];
        if (closetNum >= target) {
            return closetNum;
        }

        for (int i = 0; i < nums.length; i++) {
            for (int j = i + 1; j < nums.length; j++) {
                for (int k = j + 1; k < nums.length; k++) {
                    int threeSum = nums[i] + nums[j] + nums[k];
                    if (Math.abs(closetNum - target) > Math.abs(threeSum - target)) {
                        closetNum = threeSum;
                    }
                }
            }
        }

        return closetNum;
    }
}
```

另外一种解法为，将数组排序，控制三个数中的一个数，然后使用双指针(数组的首尾)的方法，遍历剩余的两个数，如果三个数的和与目标值更接近，则设置该值，并根据三个数的和和目标值对比，通过移动左右指针，使三个数的和更加接近目标值。

```java
class Solution {
    public int threeSumClosest(int[] nums, int target) {
        Arrays.sort(nums);
        int closetNum = nums[0] + nums[1] + nums[2];
        if (closetNum >= target) {
            return closetNum;
        }
        for (int i = 0; i < nums.length - 2; i++) {
            int left = i + 1;
            int right = nums.length - 1;

            while (left < right) {
                int threeSum = nums[i] + nums[left] + nums[right];
                if (Math.abs(closetNum - target) > Math.abs(threeSum - target)) {
                    closetNum = threeSum;
                }

                if (threeSum > target) {
                    --right;
                } else if (threeSum < target) {
                    ++left;
                } else {
                    return threeSum;
                }
            } 

        }
        return closetNum;
    }
}
```
