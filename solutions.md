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

##### 6. Encode and Decode Strings
```
class Solution:

    def encode(self, strs):
        s = ''
        for item in strs:
            count = len(item)
            s += str(count) + '#' + item
        return s

    def decode(self, s):
        strs = []
        i = 0
        while i < len(s):
            count = ''
            while s[i] != '#':
                count +=s[i]
                i+=1
            count = int(count)
            i+=1
            item = s[i: i+count]
            strs.append(item)
            i+=count
        return strs
```

##### 7. Product of Array except self
```
class Solution:
    def productExceptSelf(self, nums):
        n = len(nums)
        leftProductArray = [1] * n
        rightProductArray = [1] * n
        for i in range(1, n):
            leftProductArray[i] = leftProductArray[i-1] * nums[i-1]
        for i in range(n-2, -1, -1):
            rightProductArray[i] = rightProductArray[i+1] * nums[i+1]
        res = []
        for i in range(n):
            res.append(leftProductArray[i] * rightProductArray[i])
        return res
```

##### 8. Valid Sudoku
```
class Solution:
    def isValidSudoku(self, board):
        # check all rows
        for row in board:
            dd = set()
            for item in row:
                if item == ".": continue
                if item in dd: return False
                else: dd.add(item)
        # check all columns
        for i in range(9):
            dd = set()
            for j in range(9):
                item = board[j][i]
                if item == ".": continue
                if item in dd: return False
                else: dd.add(item)
        # check 3x3 matrices
        dd = {
            (0,0): set(),
            (0,1): set(),
            (0,2): set(),
            (1,0): set(),
            (1,1): set(),
            (1,2): set(),
            (2,0): set(),
            (2,1): set(),
            (2,2): set()
        }
        for i in range(9):
            for j in range(9):
                item = board[i][j]
                if item == ".": continue
                i_key = i//3
                j_key = j//3
                if item in dd[(i_key, j_key)]: return False
                else: dd[(i_key, j_key)].add(item)
        return True
```

##### 9. Longest consecutive sequence
```
class Solution:
    def longestConsecutive(self, nums):
        dd = set(nums)
        globalMax = 0
        for val in dd:
            if val - 1 in dd: continue
            term = val
            count = 1
            while term+1 in dd:
                term = term+1
                count+=1
            globalMax = max(globalMax, count)
        return globalMax       
```

##### 10. Valid Palindrome
```
class Solution:
    def isPalindrome(self, s: str) -> bool:
        n = len(s)
        if n <=1: return True
        filteredString = ''.join(char.lower() for char in s if char.isalnum())
        left = 0
        right = len(filteredString) - 1
        while left < right:
            if filteredString[left] != filteredString[right]: return False
            left+=1
            right-=1
        return True
```