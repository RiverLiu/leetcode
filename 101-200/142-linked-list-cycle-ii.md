# 142. 环形链表 II

- [环形链表](https://leetcode-cn.com/problems/linked-list-cycle-ii/)


先查询是否存在环，然后根据快慢指针走的位置，快指针是慢指针所走路径的2倍，从头部在找一个指针，开始遍历，与慢指针相遇的点即时入环的点.

```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode detectCycle(ListNode head) {
        if (head == null) {
            return null;
        }

        boolean hasCycle = false;
        ListNode slow = head;
        ListNode fast = head;
        while (fast.next != null && fast.next.next != null) {
            slow = slow.next;
            fast = fast.next.next;
            
            if (slow == fast) {
                hasCycle = true;
                break;
            }
        }

        if (hasCycle) {
            ListNode p = head;
            while (p != slow) {
                p = p.next;
                slow = slow.next;
            }
            return p;
        }

        return null;
    }
}
```