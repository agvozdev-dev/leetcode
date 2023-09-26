# Easy
## [1. Two Sum](https://leetcode.com/problems/two-sum/description/)

`public int[] TwoSum(int[] nums, int target) 
{
    var dictionary = Enumerable.Range(0, nums.Length).ToDictionary(i => nums[i]);

    foreach(var (value, i) in dictionary)
    {
        var result = target - value;
        if(dictionary.TryGetValue(target - value, out var j))
        {
            return new int[2]{i, j};
        }
    }

     return new int[0];
}`
