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

## [707. Design Linked List](https://leetcode.com/problems/design-linked-list/description/)

#### Решение 1. Использовал Dummy node для облегчения обработки случаев, когда нужно обрабатывать первую вершину

```cs
public class MyLinkedList 
{
    private int length;
    
    private ListNode dummy;
    
    public MyLinkedList() 
    {
        length = 1;
        dummy = new ListNode(-1);
    }
    
    public int Get(int index) 
    {
        if(IsIndexInvalid(index))
        {
            return -1;
        }
        
        var curr = dummy;
        for(var i = 0; i < index + 1; i++)
        {
            curr = curr.next;
        }
        
        return curr.val;
    }
    
    public void AddAtHead(int val) 
    {
        dummy.next = new ListNode(val, dummy.next);
        
        length++;
    }
    
    public void AddAtTail(int val) 
    {
        var curr = dummy;
        while(curr.next != null)
        {
            curr = curr.next;
        }
        
        curr.next = new ListNode(val);
        
        length++;
    }
    
    public void AddAtIndex(int index, int val) 
    {
        if(index < 0 || index > length - 1)
        {
            return;
        }
        
        var prev = dummy;
        for(int i = 0; i < index; i++)
        {
            prev = prev.next;
        }
        
        prev.next = new ListNode(val, prev.next);
        
        length++;
    }
    
    public void DeleteAtIndex(int index) 
    {
        if(IsIndexInvalid(index))
        {
            return;
        }
        
        var prev = dummy;
        for(int i = 0; i < index; i++)
        {
            prev = prev.next;
        }
            
        prev.next = prev.next.next;
        
        length--;
    }
    
    private bool IsIndexInvalid(int index)
    {
        return index < 0 || index >= length - 1;
    }
}
```

## [142. Linked List Cycle II](https://leetcode.com/problems/linked-list-cycle-ii/description/)

### Complexity: Time - O(n); Space - O(1)

#### Решение 1. Алгоритм Флойда и разница между позициями указателей

```cs
public class Solution 
{
    public ListNode DetectCycle(ListNode head)
    {
        // Получить указатель на вершину,где встретились slow и fast
        var meet = GetMeetNode(head);
        if(meet == null)
        {
            return null;
        }

        // Идем от начала связного списка до тех пор, пока не встретятся указатели.
        // Т.к. мы передвигаемся только на 1 шаг вперед за итерацию, указатели встретятся в вершине, где начинается цикл.
        var curr = head;
        while(curr != meet)
        {
            curr = curr.next;
            meet = meet.next;
        }
        
        return curr;
    }
    
    private ListNode GetMeetNode(ListNode head)
    {
        var slow = head;
        var fast = head;
        
        while(fast != null && fast.next != null)
        {
            slow = slow.next;
            fast = fast.next.next;
            
            if(slow == fast)
            {
                return slow;
            }
        }
        
        return null;
    }
}
```
