## [23. Merge k Sorted List](https://leetcode.com/problems/merge-k-sorted-lists/description/)

### Complexity: Time - O(kN); Space - O(1)
где k - число связных списков

#### Решение 1. Dummy node 

Находим индекс связного списка, который имеет на текущий момент минимальное значение. Если индекс равен -1, то это означает что мы обработали все элементы во всех связных списках и цикл нужно прерывать. 
Dummy node заводим потому что мы не знаем элемент какого из списков окажется минимальным на самой первой итерации.  

```cs
public class Solution 
{
    public ListNode MergeKLists(ListNode[] lists) 
    {
        var dummy = new ListNode(-1000000);
        
        var curr = dummy;
        while(true)
        {
            var minIndex = GetMinNodeListIndex(lists);
            if(minIndex == -1)
            {
                break;
            }
            
            curr.next = lists[minIndex];
            lists[minIndex] = lists[minIndex].next;
            
            curr = curr.next;
        }
        
        return dummy.next;
    }
    
    private int GetMinNodeListIndex(ListNode[] lists)
    {
        int minValue = 1000000;
        int minIndex = -1;
        
        for(var i = 0; i < lists.Length; i++)
        {
            var list = lists[i];
            if(list == null)
            {
                continue;
            }
            
            if(list.val < minValue)
            {
                minValue = list.val;
                minIndex = i;
            }
        }
        
        return minIndex;
    }
}
```
