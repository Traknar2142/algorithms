## Проблема
**23. Merge k Sorted Lists**\
You are given an array of k linked-lists lists, each linked-list is sorted in ascending order.

Merge all the linked-lists into one sorted linked-list and return it.

Example 1:

Input: lists = [[1,4,5],[1,3,4],[2,6]]\
Output: [1,1,2,3,4,4,5,6]\
Explanation: The linked-lists are:\
[\
1->4->5,\
1->3->4,\
2->6\
]\
merging them into one sorted list:\
1->1->2->3->4->4->5->6\
Example 2:

Input: lists = []\
Output: []\
Example 3:

Input: lists = [[]]\
Output: []

## Решение
```java
class Solution {

    public ListNode mergeKLists(ListNode[] lists) {
        //Сохдаем начальную ноду к которой будем приращивать все остальные нды
        ListNode dummy = new ListNode(0);
        ListNode current = dummy;
        while (true) {
            //Находим индекс на список с указателем на ноду с наименьшим значением
            int index = finIndexOfMinNode(lists);
            //Если прошли все ноды во всех списках, прекращаем обработку
            if (index == -1) {
                break;
            }
            //Приращиваем ноду к нашему результирующему списку
            dummy.next = lists[index];
            //Двигаем указатель списка вперед
            lists[index] = lists[index].next;
            //Двигаем указатель результирующего списка вперед
            dummy = dummy.next;
        }
        return current.next;
    }


    //Метод поиска ноды с минимальным значением в массиве свисков
    private int finIndexOfMinNode(ListNode[] lists) {
        int minVal = Integer.MAX_VALUE;
        int index = 0;
        for (int i = 0; i < lists.length; i++) {
            ListNode list = lists[i];
            if (list == null) {
                continue;
            }
            if (list.val < minVal) {
                minVal = list.val;
                index = i;
            }
        }
        if (minVal == Integer.MAX_VALUE) {
            return -1;
        } else return index;
    }
}
```
### Оценка по времени
O(n*k) где n - кол-во элементов в списке, k - количество списков в массиве
### Оценка по памяти
O(k) - хранение массивов k 
### Описание решения
1) Создается начало нашего результирующего списка dummy, к которому будем приращивать результат
2) Находим в массиве списков список, указатель которого ссылается на ноду с минимальным значением
3) Приращиваем ее к dummy и двигаем указатель dummy  вперед
4) У списка, откуда приращивали ноду, тоже двигаем указатель вперед.