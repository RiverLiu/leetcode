# 239-滑动窗口最大值

tags: 堆，滑动窗口
- https://leetcode-cn.com/problems/sliding-window-maximum/

使用堆实现，滑动窗口时，将元素移除，然后再加入新的元素。时间复杂度 $$O(N*log(N)$$

```java
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        PriorityQueue<Integer> heap = new PriorityQueue<Integer>(k, (a, b) -> b - a);
        for (int i = 0; i < k; ++i) {
            heap.offer(nums[i]);
        }

        int[] result = new int[nums.length - k + 1];
        result[0] = heap.peek();
        for (int i = k; i < nums.length; ++i) {
            heap.remove(nums[i - k]);
            heap.offer(nums[i]);
            result[i - k + 1] = heap.peek();
        }

        return result;
    }
}
```

双向队列的实现方法，在滑动窗口内，保留最大值，如果新入的元素比最大值大，则移除里面的元素，否则添加到队列中。队列头部的元素为最大值，滑动窗口时，去掉移除的元素。

PS: 难点在于临界值的判断

参考：https://time.geekbang.org/course/detail/100019701-41561

```python
class Solution(object):
    def maxSlidingWindow(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: List[int]
        """
        if not nums: return []
        window, res = [], []
        for i, x in enumerate(nums):
            if i >= k and window[0] <= i - k:
                window.pop(0)
            while window and nums[window[-1]] <= x:
                window.pop()
            window.append(i)
            if i >= k - 1:
                res.append(nums[window[0]])
        return res
```