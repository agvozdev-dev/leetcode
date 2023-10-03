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

## [91512. Number of Good Pairs](https://leetcode.com/problems/number-of-good-pairs/description/)

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
