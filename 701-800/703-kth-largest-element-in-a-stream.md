# 703-数据流中的第K大元素

- tags: 堆
- https://leetcode-cn.com/problems/kth-largest-element-in-a-stream/

采用小顶堆实现，Java提供优先队列`PriorityQueue` 默认小顶堆可实现。

```java
class KthLargest {

    private int k;
    private PriorityQueue<Integer> heap;

    public KthLargest(int k, int[] nums) {
        this.k = k;

        heap = new PriorityQueue<>(k);
        for (int num: nums) {
            add(num);
        }
    }
    
    public int add(int val) {
        if (heap.size() < k) {
            heap.offer(val);
        } else if (heap.peek() < val) {
            heap.poll();
            heap.offer(val);
        }
        
        return heap.peek();
    }
}

/**
 * Your KthLargest object will be instantiated and called as such:
 * KthLargest obj = new KthLargest(k, nums);
 * int param_1 = obj.add(val);
 */
```