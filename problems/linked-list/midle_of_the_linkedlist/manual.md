## Проблема
Given the head of a singly linked list, return the middle node of the linked list.

If there are two middle nodes, return the second middle node.

Input: head = [1,2,3,4,5]\
Output: [3,4,5]\
Explanation: The middle node of the list is node 3.
## Решение
```java
class Solution {

    public ListNode middleNode(ListNode head) {
        //Медленный указатель
        ListNode slow = head;
        //Быстрый указатель
        ListNode fast = head;
        //Проходим по всему списку, где медленный указатель сдвигается на 1 ноду
        //Быстрый сдвигается на 2 ноды пока список не закончится
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        //возвращаем медленный. Он и будет серединой списка.
        return slow;
    }

}
```
### Оценка по времени
 О(n) - линейная т.к. нужно пройти весь список до конца
### Оценка по памяти
 О(1) константная т.к. никаких дополнительных сиписков не создается
### Описание решения
Создаем два указателя - быстрый и медленный.\
Медленный двигается на одну ноду вперед за цикл.\
Быстрый двигается на две ноды за цикл.
Как только быстрый пройдет весь список до конца, меленный будет стоять на средней ноде списка
