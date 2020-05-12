# 155-最小栈

使用数组实现栈的解法，使用数组存储元素，用head标记栈顶元素的位置，如果push，就++head，并在head位置添加元素，pop就 --head，同时记录当前最小的值，在push或者 pop阶段，更新最小值 min

```
class MinStack {

    private int data[];
    private int head;
    private int min;

    /** initialize your data structure here. */
    public MinStack() {
        data = new int[8];
        head = -1;
    }
    
    public void push(int x) {
        data[++head] = x;
        if (data.length == head + 1) {
            data = Arrays.copyOf(data, data.length * 2); 
        }
        if (head == 0) {
            min = x;
        } else if (min > x) {
            min = x;
        }
    }
    
    public void pop() {
        int val = data[head];
        --head;
        if (val == min && head >= 0) {
            min = data[head];
            for (int i = head - 1; i >= 0; --i) {
                if (min > data[i]) {
                    min = data[i];
                }
            }
        }
    }
    
    public int top() {
        return data[head];
    }
    
    public int getMin() {
        return min;
    }
}
```