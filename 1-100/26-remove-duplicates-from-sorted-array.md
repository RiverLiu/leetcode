# 删除排序数组中的重复项 

- [题目链接](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)
- [领扣链接](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array/)
- [tag] Easy, Array, Two Pointers

题目很简单，用一个 `idx` 标记下数组插入的位置，然后把后面不重复的元素，插入到 `idx` 位置，`idx` 再加一.

我提交的 code，没有官方给出的代码优雅...

```java
public int removeDuplicates(int[] nums) {
    int length = nums.length;
    if (length <= 1) {
        return length;
    }
    int prefix = nums[0];
    int idx = 1;
    for (int i = 1; i < length; ++i) {
        if (prefix == nums[i]) {
            continue;
        } else {
            prefix = nums[i];
            nums[idx] = prefix;
            ++idx;
        }
    }
    
    return idx;
}
```

官方解法代码

```java
public int removeDuplicates(int[] nums) {
    if (nums.length == 0) return 0;
    int i = 0;
    for (int j = 1; j < nums.length; j++) {
        if (nums[j] != nums[i]) {
            i++;
            nums[i] = nums[j];
        }
    }
    return i + 1;
}
```

