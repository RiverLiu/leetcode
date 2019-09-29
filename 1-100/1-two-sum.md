# Two Sum 两数之和

tags: Easy, Array, Hash Table

- [题目链接](https://leetcode.com/problems/two-sum/)
- [领扣链接](https://leetcode-cn.com/problems/two-sum/)

>给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那两个整数，并返回他们的数组下标。
>
>你可以假设每种输入只会对应一个答案。但是，你不能重复利用这个数组中同样的元素。

我们先分析一下题目:

1. 数组可以包含负数，0，正数，而且数组是没有顺序的，我们不可以使用二分查找，
2. 题目要求数组中，只有一个答案，找到就可以返回。

# 解法一 暴力查找

遍历每一个元素 $$x$$，然后在查找值为 $$target - x$$ 的元素.

```java
public int[] twoSum(int[] nums, int target) {
    for (int i = 0; i < nums.length - 1; ++i) {
        int val = target - nums[i];
        for (int j = i + 1; j < nums.length; ++j) {
            if (nums[j] == val) {
                return new int[] { i, j };
            }
        }
    }

    throw new IllegalArgumentException("No two sum solution");
}
```

**复杂度分析**

- 时间复杂度 $$O(n^2)$$，两层 for 循环遍历元素
- 空间复杂度 $$O(1)$$

# 解法二 两遍哈希表(官方解法)

通过将数组中的下标和元素，放入哈希表中，元素为key，下标为 value，然后遍历数组，在哈希表中查找 $$target-x$$ 的值. 代码如下:

```java
public int[] twoSum(int[] nums, int target) {
    Map<Integer, Integer> map = new HashMap<>();
    for (int i = 0; i < nums.length; i++) {
        map.put(nums[i], i);
    }
    for (int i = 0; i < nums.length; i++) {
        int complement = target - nums[i];
        if (map.containsKey(complement) && map.get(complement) != i) {
            return new int[] { i, map.get(complement) };
        }
    }
    throw new IllegalArgumentException("No two sum solution");
}
```

**复杂度分析**

- 时间复杂度 $$O(n)$$ 两次 for 循环遍历。
- 空间复杂度 $$O(n)$$ 哈希表的大小

在讨论中，有这样一个疑问：对于数组 $$[2, 2, 3, 4, 5]$$，target 为 4 的情况， 第一个元素和第二个元素值相同，查找元素会不会出现问题？因为在Hash遍历的时候，Hash 值为 2 的对应的下标为 1，如果从头开始遍历数组，就不会出错，如果从尾部遍历数组，就会出错。

# 解法三：一遍哈希表(官方解法)

在解法二的基础上，一边查找元素，一边向哈希表中插入元素.

```java
public int[] twoSum(int[] nums, int target) {
    Map<Integer, Integer> map = new HashMap<>();
    for (int i = 0; i < nums.length; i++) {
        int complement = target - nums[i];
        if (map.containsKey(complement)) {
            return new int[] { map.get(complement), i };
        }
        map.put(nums[i], i);
    }
    throw new IllegalArgumentException("No two sum solution");
}
```

**复杂度分析**

- 时间复杂度 $$O(n)$$ 一次遍历
- 空间复杂度 $$O(n)$$ 哈希表大小 n

思考一个问题：可否先向哈希表中插入元素，在查找 $$target - x$$ 的元素？
