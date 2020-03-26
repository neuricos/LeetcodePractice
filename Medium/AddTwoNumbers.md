# Add Two Numbers

**Level:** Medium

## Description

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

## Example

```text
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.
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
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        boolean headSet = false;
        ListNode head = null;
        ListNode curr = null;
        ListNode curr1 = l1;
        ListNode curr2 = l2;
        int value;
        int remain = 0;
        while (curr1 != null && curr2 != null) {
            value = curr1.val + curr2.val + remain;
            remain = value / 10;
            value = value % 10;
            if (!headSet) {
                curr = new ListNode(value);
                head = curr;
                headSet = true;
            } else {
                curr.next = new ListNode(value);
                curr = curr.next;
            }
            curr1 = curr1.next;
            curr2 = curr2.next;
        }
        if (curr1 == null)
            curr1 = curr2;
        while (curr1 != null) {
            value = curr1.val + remain;
            remain = value / 10;
            value = value % 10;
            curr.next = new ListNode(value);
            curr = curr.next;
            curr1 = curr1.next;
        }
        if (remain != 0)
            curr.next = new ListNode(remain);
        return head;
    }
}
```

## Score

**Runtime:** 1 ms, faster than 100.00% of Java online submissions for Add Two Numbers.

**Memory Usage:** 45.3 MB, less than 76.90% of Java online submissions for Add Two Numbers.
