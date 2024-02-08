# Easy
## [1. Two Sum](https://leetcode.com/problems/two-sum/description/)

```cs
public int[] TwoSum(int[] nums, int target) 
{
    var dictionary = new Dictionary<int, int>();
    
    for(var i = 0; i < nums.Length; i++)
    {
        var result = target - nums[i];

        if(dictionary.TryGetValue(result, out var j))
        {
            return new int[2]{i, j};
        }

        dictionary.TryAdd(nums[i], i);
    }

    return new int[0];
}
```

## [9. Palindrome Number](https://leetcode.com/problems/palindrome-number/description/)

```cs
public bool IsPalindrome(int number) 
{
    var temp = number;

    var result = 0;
    while(temp > 0)
    {
        result = result * 10 + temp % 10;

        temp = (int)(temp / 10);
    }

    return number == result;
}
```

## [1512. Number of Good Pairs](https://leetcode.com/problems/number-of-good-pairs/description/)

```cs
// Сумма ряда 1+2+3+4+5... рассчитывается по формуле (n*n + n) / 2
public int NumIdenticalPairs(int[] nums) 
{
    int goodPairsCount = 0;
    var dict = new Dictionary<int, int>();

    for(var i = 0; i < nums.Length; i++)
    {
        var find = dict.TryGetValue(nums[i], out var numberCount);
        
        goodPairsCount += numberCount;

        if(find)
        {
            dict[nums[i]] = numberCount + 1;
        }
        else
        {
            dict.Add(nums[i], 1);
        }
    }

    return goodPairsCount;
}
```

## [26. Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/description/)

```cs
public int RemoveDuplicates(int[] nums) 
{
    int k = 1;
    var min = nums[0];

    for(int i = 1; i < nums.Length; i++)
    {
        if(min != nums[i])
        {
            nums[k++] = nums[i];
        }

        min = nums[i];
    }

    return k;
}
```

## [27. Remove Element](https://leetcode.com/problems/remove-element/description/)

```cs
public int RemoveElement(int[] nums, int val) 
{
    int result = 0;

    for(int i = 0; i < nums.Length; i++)
    {
        if(nums[i] != val)
        {
            nums[result++] = nums[i];
        }
    }

    return result;
}
```

## [28. Find the Index of the First Occurrence in a String](https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/description/)

### Решение 1. Прямой поиск (O(M*N))

```cs
public int StrStr(string haystack, string needle) 
{
    for(int i = 0; i < haystack.Length - needle.Length + 1; i++)
    {
        bool find = true;
        for(int j = 0; j < needle.Length; j++)
        {
            if(haystack[i+j] != needle[j])
            {
                find = false;
                break;
            }
        }

        if(find)
        {
            return i;
        }
    }
    
    return -1;
}
```

## [125. Valid Palindrome](https://leetcode.com/problems/valid-palindrome/description/)

### Complexity: Time - O(n); Space - O(n)

```cs
public bool IsPalindrome(string s) 
{
    var left = 0;
    var right = s.Length - 1;

    while(left <= right)
    {
        if(!char.IsLetterOrDigit(s[left]))
        {
            left++;
            continue;
        }

        if(!char.IsLetterOrDigit(s[right]))
        {
            right--;
            continue;
        }

        if(Char.ToLower(s[left++]) != Char.ToLower(s[right--]))
        {
            return false;
        }
    }

    return true;
}
```

## [20. Valid Parentheses](https://leetcode.com/problems/valid-parentheses/description/?source=submission-ac)

### Complexity: Time - O(n); Space - O(1)
```cs
public bool IsValid(string s) 
{
    if(s.Length % 2 != 0)
    {
        return false;
    }

    var bracketsMap = new Dictionary<char, char>
    {
        {')', '('},
        {'}', '{'},
        {']', '['},
    };
    
    var openBrackets = new Stack<char>();
    foreach(var current in s)
    {
        if(!bracketsMap.TryGetValue(current, out var openBracket))
        {
            openBrackets.Push(current);
            continue;
        }

        if(openBrackets.TryPop(out var topStackBracket) && openBracket == topStackBracket)
        {
            continue;
        }

        return false;
    }

    return openBrackets.Count == 0;
}
```

## [2824. Count Pairs Whose Sum is Less than Target](https://leetcode.com/problems/count-pairs-whose-sum-is-less-than-target/description/)
##### Topics: Array | Two Pointers | Binary Search | Sorting
##### Complexity: Time - O(NLog(N)) + O(n); Space - O(1)
```cs
public int CountPairs(IList<int> nums, int target) 
{
    nums = nums.OrderBy(x => x).ToList();

    var count = 0;
    for(int left = 0, right = nums.Count - 1; left <= right;)
    {
        var sum = nums[left] + nums[right];
        if(sum >= target)
        {
            right--;
        }
        else
        {
            // т.к. массив отсортирован, числа перед right <= right, а значит сумма не будет превышать пороговое значение
            count += right - left;
            left++;
        }
    }

    return count;
}
```
