# 25-K 个一组翻转链表

https://leetcode-cn.com/problems/reverse-nodes-in-k-group/

先分组，在进行反转，记录上一组的未节点，然后再拼接。难点在于，节点之间的拼接

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
    public ListNode reverseKGroup(ListNode head, int k) {
        if (head == null || k == 1) {
            return head;
        }

        ListNode start = head;
        ListNode before = null;
        while (start != null) {
            int cnt = k;
            ListNode end = start;
            while (--cnt > 0 && end != null) {
                end = end.next;
            }
            if (cnt > 0 || end == null) {
                break;
            }

            if (before != null) {
                before.next = end;
            } else {
                head = end;
            }
            before = start;

            // start to reverse
            ListNode current = start;
            ListNode next = current.next;
            current.next = end.next;
            while (current != end) {
                start = next.next;
                next.next = current;
                current = next;
                next = start;
            }
        }

        return head;
    }
}
```