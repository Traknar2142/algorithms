## Проблема
**234. Palindrome Linked List**\
Given the head of a singly linked list, return true if it is a
palindrome or false otherwise.

Input: head = [1,2,2,1]\
Output: true

Input: head = [1,2]\
Output: false


## Решение 
```java
class Solution {
    public boolean isPalindrome(ListNode head) {
        //Ищем середину списка - ноду после которой будем разворачивать список
        ListNode middleNode = getMiddleNode(head);
        /*разворачивает вторую половину связанного списка
          Пример:      
          head: 1 -> 2 -> 3 -> 2 -> 1 -> null
          после реверса
          head: 1 -> 2 -> null <- 3 <- 2 <- 1
         */
        ListNode reverseLastPart = reverseList(middleNode);
        ListNode traverseNode = head;
        ListNode traverseMiddle = reverseLastPart;

        boolean isPalindrome = true;

        //Идем с двух сторон связного списка, 
        // сравнивая элементы, пока один из концов не упрется в null
        while (traverseNode !=null && traverseMiddle != null) {
            if (traverseNode.val != traverseMiddle.val){
                isPalindrome = false;
            }
            traverseNode = traverseNode.next;
            traverseMiddle = traverseMiddle.next;
        }
        reverseList(reverseLastPart);
        return isPalindrome;

    }

    private ListNode getMiddleNode(ListNode head){
        ListNode slow = head;
        ListNode fast = head;
        while (fast !=null && fast.next != null){
            slow = slow.next;
            fast = fast.next.next;
        }
        return slow;
    }

    private ListNode reverseList(ListNode head){
        ListNode current = head;
        ListNode prev = null;
        ListNode tmp;
        while(current != null){
            tmp = current;
            current = current.next;
            tmp.next = prev;
            prev = tmp;
        }
        return prev;
    }
}
```
### Оценка по времени
О(n) - линейная т.к. как минимум нужно проверить все ноды списка, если список является полиндромом
### Оценка по памяти
O(1) - константная т.к ничего нового не порождаем.
### Описание решения
1) Находим середину списка с помощью паттерна быстрый/медленный указатель
2) Берем среднюю ноду и переопределяем направление списка
3) Идем с двух сторон списка, сравнивая элементы, пока один из указателей не вернет null
4) Разворачивам вторую половину обратно, чтобы список вернулся в изначальную форму
5) Возвращаем булевло isPalindrome