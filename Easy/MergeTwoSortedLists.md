# Merge Two Sorted Lists

**Level:** Easy

## Description

Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

## Example

```text
Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4
```

## Solution

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
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if (l1 == null && l2 == null)
            return null;

        ListNode head = null;
        ListNode curr = null;
        ListNode tmp  = null;
        ListNode n1 = l1;
        ListNode n2 = l2;

        while (n1 != null && n2 != null) {
            int v1 = n1.val;
            int v2 = n2.val;

            if (v1 <= v2) {
                tmp = new ListNode(v1);
                n1 = n1.next;
            } else {
                tmp = new ListNode(v2);
                n2 = n2.next;
            }
            if (head == null) {
                head = tmp;
                curr = head;
            } else {
                curr.next = tmp;
                curr = curr.next;
            }
        }

        tmp = (n1 == null)? n2:n1;
        while (tmp != null) {
            if (head == null) {
                head = new ListNode(tmp.val);
                curr = head;
            } else {
                curr.next = new ListNode(tmp.val);
                curr = curr.next;
            }
            tmp = tmp.next;
        }

        return head;
    }
}
```

## Score

**Runtime:** 1 ms, faster than 20.57% of Java online submissions for Merge Two Sorted Lists.\
**Memory Usage:** 39.7 MB, less than 16.16% of Java online submissions for Merge Two Sorted Lists.
