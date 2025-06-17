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

##### 4. Group Anagrams
```
class Solution:
    def groupAnagrams(self, strs):
        dd = {}
        for item in strs:
            signatureArr = [0] * 26
            for char in item:
                k = ord(char) - ord('a')
                signatureArr[k] +=1
            signatureTuple = tuple(signatureArr)
            if signatureTuple in dd: dd[signatureTuple].append(item)
            else: dd[signatureTuple] = [item]
        return list(dd.values())
```

##### 5. Top K frequent elements
```
import heapq
class Solution:
    def topKFrequent(self, nums, k):
        dd = {}
        for i in nums:
            freq = dd.get(i, 0)
            dd[i] = freq+1
        heap = []
        for key, freq in dd.items():
            heapq.heappush(heap, (-freq, key))
        res = []
        for i in range(k):
            _, key = heapq.heappop(heap)
            res.append(key)
        return res
```