# 移除元素

tags: Easy, Array, Two Pointers

- [题目链接](https://leetcode.com/problems/remove-element/)
- [领扣链接](https://leetcode-cn.com/problems/remove-element/)

把出现的数组中的元素移除掉，只需要遍历数组，把不一样的数组向前移动即可.

```java
    public int removeElement(int[] nums, int val) {
        int idx = 0;
        for (int i = 0; i < nums.length; ++i) {
            if (nums[i] != val) {
                nums[idx] = nums[i];
                ++idx;
            }
        }
        return idx;
    }
```

**复杂度分析**

- 时间复杂度: $$O(n)$$ 一层遍历
- 空间复杂度: $$O(1)$$
