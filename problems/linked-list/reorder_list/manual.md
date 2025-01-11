## Проблема
**143. Reorder List**\
ou are given the head of a singly linked-list. The list can be represented as:

L0 → L1 → … → Ln - 1 → Ln
Reorder the list to be on the following form:

L0 → Ln → L1 → Ln - 1 → L2 → Ln - 2 → …
You may not modify the values in the list's nodes. Only nodes themselves may be changed.

Input: head = [1,2,3,4]\
Output: [1,4,2,3]

Input: head = [1,2,3,4,5]\
Output: [1,5,2,4,3]

Constraints:

The number of nodes in the list is in the range [1, 5 * 104].\
1 <= Node.val <= 1000
## Решение
```java
class Solution {
    public void reorderList(ListNode head) {
        //Находим ноду перед центральной
        ListNode tmp = getPreMid(head);
        //Делаем ревеср нод после найденой
        ListNode reverseSecondPart = reverse(tmp.next);
        //зануляем предсрединную ноду, чтобы разделить список на 2 половины
        //1 -> 2 -> 3 -> null null <- 4 <- 5 <- 6
        tmp.next = null;

        //Формируем указатели для итерации
        //1 -> 2 -> 3 -> null null <- 4 <- 5 <- 6
        //^                                     ^
        //p1                                    p2
        ListNode p2 = reverseSecondPart;
        ListNode p1 = head;

        //каждый цикл меняем указатели местами со сдвигом на 1 ноду для реордеринга
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
            tmp.next = prev;
            prev = tmp;
        }
        return prev;
    }
}
```
### Оценка по времени
O(n) - линейная т.к. нужно прийти по всем нодам для реордеринга
### Оценка по памяти
O(1) - константная т.к никакой дополнительной памяти для решения задачи не выделяется.

### Описание решения
В комментарии кода