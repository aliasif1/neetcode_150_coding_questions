##### 1. Contains Duplicate
```
class Solution:
    def hasDuplicate(self, nums):
        numsSet = set()
        for x in nums:
            if x in numsSet: return True
            numsSet.add(x)
        return False
```

##### 2. Valid Anagram
```
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        dd = {}
        for char in s:
            freq = dd.get(char, 0)
            dd[char] = freq+1
        for char in t:
            freq = dd.get(char, 0)
            if freq == 0: return False
            elif freq == 1: dd.pop(char)
            else: dd[char] = freq-1
        if len(dd) !=0: return False
```

##### 3. Two Sum
```
class Solution:
    def twoSum(self, nums, target):
        dd = {}
        for i in range(len(nums)):
            val = target-nums[i]
            if val in dd: return [dd[val], i]
            else: dd[nums[i]] = i
        return []
            
```