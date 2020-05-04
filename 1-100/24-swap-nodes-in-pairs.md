# 24-两两交换链表中的节点

- [力抠](https://leetcode-cn.com/problems/swap-nodes-in-pairs/)


```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode swapPairs(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }

        ListNode current = head;
        ListNode next = head.next;
        head = next;

        ListNode before = null;
        while(next != null) {
            // 交换当前
            current.next = next.next;
            next.next = current;

            // 与上两个连接
            if (before != null) {
                before.next = next;
            }
            before = current;
        
            // 寻找下一轮
            current = current.next;
            if (current == null) {
                break;
            } else {
                next = current.next;
            }
        }

        return head;
    }
}
```