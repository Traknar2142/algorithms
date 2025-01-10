## Проблема
**19. Remove Nth Node From End of List**

Given the head of a linked list, remove the nth node from the end of the list and return its head.

Input: head = [1,2,3,4,5], n = 2\
Output: [1,2,3,5]

Input: head = [1], n = 1\
Output: []

Input: head = [1,2], n = 1\
Output: [1]
## Решение 
```java
public class Solution {

    public ListNode removeNthFromEnd(ListNode head, int n) {
        //Создаем ноду-заглушку для крайнего случая, если убираем первый элемент
        //и лист состоит из одного элемента
        ListNode dummy = new ListNode(0, head);

        //Считаем колличесвто элементов в листе вместе с нодой-заглушкой
        int lenght = 0;
        ListNode counter = dummy;
        while (counter != null) {
            lenght++;
            counter = counter.next;
        }

        // находим нужную ноду для переопределения ссылки по формуле 
        //length - n - 1
        counter = dummy;
        for (int i = 0; i < lenght - n - 1; i++){
            counter = counter.next;
        }

        //переопределяем ссылки ноды
        counter.next = counter.next.next;
        return dummy.next;
    }

}
```
### Оценка по времени
О(n) - линейная т.к один проход совершаем для подсчета элементов, второй для нахождения нужной ноды и ее переопределения

### Оценка по памяти
О(1) - константная т.к. манипуляции проводим с предоставленным списком и новые не порождаем
### Описание решения
Создаем dummy заглушку для случая, когда список состоит из одной ноды. Она будет первым элементом в списке\
Итерируемся по списку в первый раз чтобы посчитать колличество элементов в списке\
Итерируемся по списку ```lenght - n - 1``` раз чтобы найти ноду, которую будем переопределять\
Совершаем переопределние ноды.
