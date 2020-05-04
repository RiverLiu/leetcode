# 232-用栈实现队列

tags: 栈, 设计

- https://leetcode-cn.com/problems/implement-queue-using-stacks/

Java. Java 提供的栈 Stack， 该类继承 Vector，Vector底层使用数组实现，可以参照 Stack 的实现，修改下获取元素的顺序就可以实现队列的功能。

```cpp
class MyQueue {

    private Stack<Integer> stack;

    /** Initialize your data structure here. */
    public MyQueue() {
        stack = new Stack<>();
    }
    
    /** Push element x to the back of queue. */
    public void push(int x) {
        stack.add(x);
    }
    
    /** Removes the element from in front of queue and returns that element. */
    public int pop() {
        return stack.remove(0);
    }
    
    /** Get the front element. */
    public int peek() {
        return stack.get(0);
    }
    
    /** Returns whether the queue is empty. */
    public boolean empty() {
        return stack.isEmpty();
    }
}
```
