## [23. Merge k Sorted List](https://leetcode.com/problems/merge-k-sorted-lists/description/)

### Complexity: Time - O(kN); Space - O(1)
где k - число связных списков

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
