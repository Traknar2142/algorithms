## Проблема
**21. Merge Two Sorted Lists**\
You are given the heads of two sorted linked lists list1 and list2.

Merge the two lists into one sorted list. The list should be made by splicing together the nodes of the first two lists.

Return the head of the merged linked list.

Input: list1 = [1,2,4], list2 = [1,3,4]\
Output: [1,1,2,3,4,4]

Example 2:

Input: list1 = [], list2 = []\
Output: []

Example 3:

Input: list1 = [], list2 = [0]\
Output: [0]

## Решение
```java
class Solution {

    public ListNode mergeTwoLists(ListNode list1, ListNode list2) {
        //Создаем дефолтную ноду, к которой будем приращивать результат
        ListNode dummy = new ListNode(0);
        //Сохраняем указатель на голову
        ListNode result = dummy;

        //Пока не пройдем все ноды в списках
        while (list1 != null || list2 != null) {
            //Сравниваем значение нод
            //Ноду с наименьшим значением приращиваем к dummy и двигаем указатели вперед
            if (getVal(list1) < getVal(list2)) {
                dummy.next = list1;
                list1 = list1.next;
            } else {
                dummy.next = list2;
                list2 = list2.next;
            }

            dummy = dummy.next;
        }
        return result.next;
    }

    //Метод для извлечения значения из ноды
    public int getVal(ListNode node) {
        if (node == null) {
            return Integer.MAX_VALUE;
        } else {
            return node.val;
        }
    }
}
```
### Оценка по времени
О(n) - нужно обойти все ноды списков
### Оценка по памяти
O(1) - константная т.к. задано строго 2 списка.
### Описание решения
1) Создаем дефолтную ноду dummy, к которой будем приращивать результат
2) Проходим по обоим спискам, пока указатели в обоих списках не станут null
3) Сравниваем значения в указателях обоих списках. Наименьший приращиваем к dummy и оба указателя двигаем вперед
4) Возвращаем Сформированный список вызывая result.next;