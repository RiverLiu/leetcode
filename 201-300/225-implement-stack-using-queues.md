# 225-用队列实现栈

tags: 栈，设计

- https://leetcode-cn.com/problems/implement-stack-using-queues/

使用双向队列实现栈的功能.


```java
class MyStack {

    private ArrayDeque<Integer> queue;

    /** Initialize your data structure here. */
    public MyStack() {
        queue = new ArrayDeque<>();
    }
    
    /** Push element x onto stack. */
    public void push(int x) {
        queue.addLast(x);
    }
    
    /** Removes the element on top of the stack and returns that element. */
    public int pop() {
        return queue.pollLast();
    }
    
    /** Get the top element. */
    public int top() {
        return queue.peekLast();
    }
    
    /** Returns whether the stack is empty. */
    public boolean empty() {
        return queue.isEmpty();
    }
}
```