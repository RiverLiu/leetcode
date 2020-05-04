# 反转链表



自己的解法. 遇到的问题是，如何设置下一次查找的节点和判断结束的条件.

在原有链表的基础上，通过增加两个指向节点的指针解决。

另外的思路，通过将链表压入栈中，然后出栈，可以实现反转的目的，占用额外空间和时间.

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
    public ListNode reverseList(ListNode head) {
        if (head == null) {
            return head;
        }
        ListNode current = head;
        ListNode next = current.next;
        current.next = null;
        while (next != null) {
            head = next.next;

            next.next = current;
            current = next;
            next = head;
        }

        return current;
    }
}
```





