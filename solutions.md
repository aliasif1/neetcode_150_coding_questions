##### 1. Contains Duplicate
```
class Solution:
    def hasDuplicate(self, nums):
        dd = {}
        for x in nums:
            if x in dd: return True
            else: dd[x] = True
        return False
```