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

##### 11. Two Sum 2 Input Array is Sorted 
```
class Solution:
    def twoSum(self, numbers, target):
        left = 0
        right = len(numbers) - 1
        while left < right:
            total = numbers[left] + numbers[right]
            if total == target: return [left + 1, right + 1]
            elif total < target: left+=1
            else: right-=1
```

##### 12. 3Sum 
```
class Solution:
    def threeSum(self, nums):
        n = len(nums)
        if n < 3: return []
        nums.sort(reverse=True)
        res = []
        i = 0
        lastVal = None
        for i in range(n-2):
            if nums[i] == lastVal: continue
            j = i+1
            k = n-1
            while j < k:
                total = nums[i] + nums[j] + nums[k]
                if total == 0:
                    res.append([nums[i], nums[j], nums[k]])
                    j+=1
                    k-=1
                    while j < k and nums[j] == nums[j-1]: j+=1
                    while j < k and nums[k] == nums[k+1]: k-=1
                elif total > 0:
                    j+=1
                else:
                    k-=1
            lastVal = nums[i]
        return res
```

##### 13. Container with most water 
```
class Solution:
    def maxArea(self, heights):
        left = 0
        right = len(heights) - 1
        globalMax = 0
        while left < right:
            capacity = (right - left) * min(heights[left], heights[right])
            globalMax = max(globalMax, capacity)
            if heights[left] <= heights[right]: left+=1
            else: right-=1
        return globalMax
```

##### 14. Trapping Rain water 
```
class Solution:
    def trap(self, height):
        left = 0
        right = len(height) - 1
        maxLeft = 0
        maxRight = 0
        totalWater = 0
        while left <= right:
            if maxLeft <= maxRight:
                totalWater +=max(maxLeft - height[left], 0)
                maxLeft = max(maxLeft, height[left])
                left+=1
            else:
                totalWater +=max(maxRight - height[right], 0)
                maxRight = max(maxRight, height[right])
                right-=1
        return totalWater
```

##### 1-D Dynamic Programing
##### Climbing Stairs (Recursion)
##### Concept: climbStairs(n) = climbStairs(n-1) + climbStairs(n-2)
```
class Solution:
    def climbStairs(self, n: int) -> int:
        def climb(n, memo = {}):
            if n == 0: return 1
            if n == 1: return 1
            if n in memo: return memo[n]
            memo[n] = climb(n-1, memo) + climb(n-2, memo)
            return memo[n]
        return climb(n)
```

##### 1-D Dynamic Programing
##### Climbing Stairs (DP Table)
##### Concept: climbStairs(n) = climbStairs(n-1) + climbStairs(n-2)
```
class Solution:
    def climbStairs(self, n: int) -> int:
        if n == 0: return 1
        if n == 1: return 1
        a,b = 1, 1
        for i in range(2, n+1):
            a,b = b, a+b
        return b
```

##### 1-D Dynamic Programing
##### Min Cost Climbing Stairs (Recursion)
##### Concept: minCostClimbingStairs(n) = min[cost(n-1) + minCostClimbingStairs(n-1), cost(n-2) + minCostClimbingStairs(n-2)]
##### base case: minCostClimbingStairs(0) = 0 and minCostClimbingStairs(1) = 0
```
class Solution:
    def minCostClimbingStairs(self, cost) -> int:
        def recur(i, memo = {}):
            if i == 0: return 0
            if i == 1: return 0
            if i in memo: return memo[i]
            memo[i] = min( (cost[i-1] + recur(i-1, memo) ), (cost[i-2] + recur(i-2, memo) ) )
            return memo[i]
        
        n = len(cost)
        if n <= 1: return 0
        return recur(n)
```

##### 1-D Dynamic Programing
##### Min Cost Climbing Stairs (DP Table)
##### Concept: minCostClimbingStairs(n) = min[cost(n-1) + minCostClimbingStairs(n-1), cost(n-2) + minCostClimbingStairs(n-2)]
##### base case: minCostClimbingStairs(0) = 0 and minCostClimbingStairs(1) = 0
```
class Solution:
    def minCostClimbingStairs(self, cost) -> int:
        n = len(cost)
        a,b = 0, 0
        for i in range(2, n+1):
            a,b = b, min((a + cost[i-2]), (b + cost[i-1]))
        return b
```