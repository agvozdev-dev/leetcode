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

## [143. Reorder List](https://leetcode.com/problems/reorder-list/description/)

### Complexity: Time - O(n); Space - O(1)

#### Решение 1. Dummy node + fast & slow pointers

```cs
public void ReorderList(ListNode head) 
{
    var middle = GetMiddleNode(head);

    var l1 = head;
    var l2 = GetReversedSublistHead(middle);

    while(l2.next != null)
    {
        var temp = l1.next;
        l1.next = l2;
        l1 = temp;

        temp = l2.next;
        l2.next = l1;
        l2 = temp;
    }
}

private ListNode GetMiddleNode(ListNode head)
{
    var fast = head;
    var slow = head;

    while(fast != null && fast.next != null)
    {
        slow = slow.next;
        fast = fast.next.next;
    }

    return slow;
}

private ListNode GetReversedSublistHead(ListNode middle)
{
    ListNode prev = null;
    
    var curr = middle;
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
