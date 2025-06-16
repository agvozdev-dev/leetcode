# Medium

## [19. Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/description/)

### Complexity: Time - O(n); Space - O(1)

#### Решение 1. Dummy node + fast & slow pointers

Нужно удалить n-ую вершину с конца:

1. Быстрый указатель передвигаем на n+1 позицию (+1 потому что есть dummy node).
2. Двигаем оба указателя до тех пор, пока fast != null.

В результате slow-указатель будет указывать на нужную нам вершину - ту, которая перед удаляемой. Другими словами, мы организовали между ними нужное нам расстояние. 

```cs
public ListNode RemoveNthFromEnd(ListNode head, int n) 
{
    var dummy = new ListNode(0, head);

    var fast = dummy;
    for(var i = 0; i < n + 1; i++) // n + 1, т.к. есть dummy node
    {
        fast = fast.next;
    }

    var slow = dummy;
    while(fast != null)
    {
        fast = fast.next;
        slow = slow.next;
    }

    slow.next = slow.next.next;

    return dummy.next;
}
```

Совпали названия, это не алгоритм быстрого и медленного указателя.

#### Решение 2. Dummy node
```cs
public ListNode RemoveNthFromEnd(ListNode head, int n) 
{
    var dummy = new ListNode(0, head);

    var curr = dummy;
    var length = 0;

    while(curr != null)
    {
        length++;
        curr = curr.next;
    }

    curr = dummy;
    for(int i = 0; i < length - n - 1; i++)
    {
        curr = curr.next;
    }

    curr.next = curr.next.next;

    return dummy.next;
}
```

## [206. Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/description/)

### Complexity: Time - O(n); Space - O(1)

#### Решение 1. Итеративное

У нас нет указателя на предыдущий элемент. Значит,нам нужно его где-то сохранять заранее. Также на нужно сохранять указатель на следующий элемент, т.к. связь текущего со следующим мы разорвем. 

1. Заводим указатель на предыдущий элемент - prev.
2. Заводим указатель на следующий элемент - next.

В конце каждой итерации цикла prev указывает на предыдущий элемент, а curr и next на один и тот же - текущий. 

```cs
public ListNode ReverseList(ListNode head) 
{
    var curr = head;
    ListNode prev = null;

    while(curr != null)
    {
        var next = curr.next;
        curr.next = prev;
        prev = curr;
        curr = next;
    }

    return prev;
}
```

## [876. Middle of the Linked List](https://leetcode.com/problems/middle-of-the-linked-list/description/)

### Complexity: Time - O(n); Space - O(1)

#### Решение 1. Быстрый и медленный указатели

1. Заводим два указателя - fast и slow, которые указывают на head.
2. Fast движется в два раза быстрее.
3. Как только fast дошел до конца, slow окажется на середине связного списка.

```cs
public ListNode MiddleNode(ListNode head) 
{
    var fast = head;
    var slow = head;

    while(fast != null && fast.next != null)
    {
        // slow сдвигаем на одну позицию, а fast - на две.
        slow = slow.next;
        fast = fast.next.next;
    }

    return slow;
}
```
