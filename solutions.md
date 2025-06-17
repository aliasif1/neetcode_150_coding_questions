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