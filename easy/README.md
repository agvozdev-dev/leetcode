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
