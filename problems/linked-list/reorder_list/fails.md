Решения, которые зафейлены

```java
class Solution {

    public void reorderList(ListNode head) {
        ListNode tmp = getPreMid(head);

        ListNode reverseSecondPart = reverse(tmp.next);
        tmp.next = null;

        ListNode p2 = reverseSecondPart;
        
        // ЗДЕСЬ ДОЛЖЕН БЫТЬ HEAD Т.К. ИДЕМ С ГОЛОВЫ
        ListNode p1 = tmp;

        ListNode p1_next;
        while (p2 != null) {
            p1_next = p1.next;
            p1.next = p2;
            p1 = p2;
            p2 = p1_next;
        }

    }


    private ListNode getPreMid(ListNode head) {
        ListNode slow = head;
        ListNode fast = head;

        while (fast != null && fast.next != null && fast.next.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        return slow;
    }


    private ListNode reverse(ListNode head) {
        ListNode curr = head;
        ListNode prev = null;
        ListNode tmp;

        while (curr != null) {
            tmp = curr;
            curr = curr.next;
            temp.next = prev;
            prev = tmp;
        }
        return prev;
    }

}
```