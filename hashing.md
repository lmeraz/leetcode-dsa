# Declaration: a hash map is declared like any other variable. The syntax is {}
hash_map = {}

# If you want to initialize it with some key value pairs, use the following syntax:
hash_map = {1: 2, 5: 3, 7: 2}

# Checking if a key exists: simply use the `in` keyword
1 in hash_map # True
9 in hash_map # False

# Accessing a value given a key: use square brackets, similar to an array.
hash_map[5] # 3

# Adding or updating a key: use square brackets, similar to an array.
# If the key already exists, the value will be updated
hash_map[5] = 6

# If the key doesn't exist yet, the key value pair will be inserted
hash_map[9] = 15

# Deleting a key: use the del keyword. Key must exist or you will get an error.
del hash_map[9]

# Get size
len(hash_map) # 3

# Get keys: use .keys(). You can iterate over this using a for loop.
keys = hash_map.keys()
for key in keys:
    print(key)

# Get values: use .values(). You can iterate over this using a for loop.
values = hash_map.values()
for val in values:
    print(val)

## Checking for existence
Example 1: 1. Two Sum
https://leetcode.com/problems/two-sum/
Given an array of integers nums and an integer target, return indices of two numbers such that they add up to target. You cannot use the same index twice.

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        dic = {}
        for i in range(len(nums)):
            num = nums[i]
            complement = target - num
            if complement in dic: # This operation is O(1)!
                return [i, dic[complement]]
            
            dic[num] = i
        
        return [-1, -1]
```

Example 2: 2351. First Letter to Appear Twice

Given a string s, return the first character to appear twice. It is guaranteed that the input will have a duplicate character.
https://leetcode.com/problems/first-letter-to-appear-twice/description/
```
2351. First Letter to Appear Twice
Easy

Topics

Companies

Hint
Given a string s consisting of lowercase English letters, return the first letter to appear twice.

Note:

A letter a appears twice before another letter b if the second occurrence of a is before the second occurrence of b.
s will contain at least one letter that appears twice.
 

Example 1:

Input: s = "abccbaacz"
Output: "c"
Explanation:
The letter 'a' appears on the indexes 0, 5 and 6.
The letter 'b' appears on the indexes 1 and 4.
The letter 'c' appears on the indexes 2, 3 and 7.
The letter 'z' appears on the index 8.
The letter 'c' is the first letter to appear twice, because out of all the letters the index of its second occurrence is the smallest.
Example 2:

Input: s = "abcdd"
Output: "d"
Explanation:
The only letter that appears twice is 'd' so we return 'd'.
 

Constraints:

2 <= s.length <= 100
s consists of lowercase English letters.
s has at least one repeated letter.
```

```python
class Solution:
    def repeatedCharacter(self, s: str) -> str:
        seen = set()
        for c in s:
            if c in seen:
                return c
            seen.add(c)

        return " "
```


Example 3: Given an integer array nums, find all the unique numbers x in nums that satisfy the following: x + 1 is not in nums, and x - 1 is not in nums.

```python
def find_numbers(nums):
    ans = []
    nums = set(nums)

    for num in nums:
        if (num + 1 not in nums) and (num - 1 not in nums):
            ans.append(num)
    
    return ans
```

```Anytime you find your algorithm running if ... in ..., then consider using a hash map or set to store elements to have these operations run in 
O
(
1
)
O(1). Try these upcoming practice problems with what was learned here.
```

```
Largest Unique Number
Given an integer array nums, return the largest integer that only occurs once. If no integer occurs once, return -1.

 

Example 1:

Input: nums = [5,7,3,9,4,9,8,3,1]
Output: 8
Explanation: The maximum integer in the array is 9 but it is repeated. The number 8 occurs only once, so it is the answer.
Example 2:

Input: nums = [9,9,8,8]
Output: -1
Explanation: There is no number that occurs only once.
 

Constraints:

1 <= nums.length <= 2000
0 <= nums[i] <= 1000
```
```python
from collections import defaultdict
class Solution:
    def largestUniqueNumber(self, nums: List[int]) -> int:
        cts = defaultdict(int)
        for num in nums:
            cts[num] +=1
        ans = -1
        for k,v in cts.items():
            if v==1:
                ans = max(ans,k)
        return ans
```

```
Given a string text, you want to use the characters of text to form as many instances of the word "balloon" as possible.

You can use each character in text at most once. Return the maximum number of instances that can be formed.

 

Example 1:



Input: text = "nlaebolko"
Output: 1
Example 2:



Input: text = "loonbalxballpoon"
Output: 2
Example 3:

Input: text = "leetcode"
Output: 0
 

Constraints:

1 <= text.length <= 104
text consists of lower case English letters only.
```
```
from collections import defaultdict
class Solution:
    def maxNumberOfBalloons(self, text: str) -> int:
        cts = defaultdict(int)
        for c in text:
            cts[c] +=1
        b = {'b':1,'a':1,'l':2,'o':2,'n':1}
        ct = [0]* len('balon')
        for i,(letter, required) in enumerate(b.items()):
            ct[i] = cts[letter]//required
        return min(ct)
```
```
Given a binary array nums, return the maximum length of a contiguous subarray with an equal number of 0 and 1.
```
```python
class Solution:
    def findMaxLength(self, nums: List[int]) -> int:
        # dictionary
        prefixSum = {0: -1}
        total = 0
        maxlength = 0
        
        for index, value in enumerate(nums):
            if value == 0:
                total -= 1
            else:
                total += 1
            if total not in prefixSum.keys():
                prefixSum[total] = index
            else:
                maxlength = max(maxlength, index-prefixSum[total])        
        return maxlength
``````
```
Example 1: 49. Group Anagrams

Given an array of strings strs, group the anagrams together.

For example, given strs = ["eat","tea","tan","ate","nat","bat"], return [["bat"],["nat","tan"],["ate","eat","tea"]].
```
```python
from collections import defaultdict

class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        groups = defaultdict(list)
        for s in strs:
            key = "".join(sorted(s))
            groups[key].append(s)
        
        return groups.values()
```
```
Example 2: 2260. Minimum Consecutive Cards to Pick Up

Given an integer array cards, find the length of the shortest subarray that contains at least one duplicate. If the array has no duplicates, return -1.
```
```python
from collections import defaultdict

class Solution:
    def minimumCardPickup(self, cards: List[int]) -> int:
        dic = defaultdict(list)
        for i in range(len(cards)):
            dic[cards[i]].append(i)
            
        ans = float("inf")
        for key in dic:
            arr = dic[key]
            for i in range(len(arr) - 1):
                ans = min(ans, arr[i + 1] - arr[i] + 1)
        
        return ans if ans < float("inf") else -1
// or
from collections import defaultdict

class Solution:
    def minimumCardPickup(self, cards: List[int]) -> int:
        dic = defaultdict(int)
        ans = float("inf")
        for i in range(len(cards)):
            if cards[i] in dic:
                ans = min(ans, i - dic[cards[i]] + 1)
            
            dic[cards[i]] = i

        return ans if ans < float("inf") else -1
```
```
Example 3: 2342. Max Sum of a Pair With Equal Sum of Digits

Given an array of integers nums, find the maximum value of nums[i] + nums[j], where nums[i] and nums[j] have the same digit sum (the sum of their individual digits). Return -1 if there is no pair of numbers with the same digit sum.
```
```python
from collections import defaultdict
def func():
    def get_digit_sum(num):
        digit_sum = 0
        while num:
            digit_sum += num%10
            num //=10
    d = defaultdict(int)
    for num in nums:
        digit_sum = get_digit_sum(num)
        if digit_sum in d:
            ans = max(ans, num+d[digit_sum])
        d[digit_sum] = max(d[digit_sum], num)
    ans = -1
    for k in d:
        c= d[k]
        if len(c) >1:
            c.sort(reverse=True)
            ans = max(ans, c[0]+c[1])
    return ans

```
```
Example 4: 2352. Equal Row and Column Pairs

Given an n x n matrix grid, return the number of pairs (R, C) where R is a row and C is a column, and R and C are equal if we consider them as 1D arrays.
```
```python
from collections import defaultdict

class Solution:
    def equalPairs(self, grid: List[List[int]]) -> int:
        def convert_to_key(arr):
            # Python is quite a nice language for coding interviews!
            return tuple(arr)
        
        dic = defaultdict(int)
        for row in grid:
            dic[convert_to_key(row)] += 1
        
        dic2 = defaultdict(int)
        for col in range(len(grid[0])):
            current_col = []
            for row in range(len(grid)):
                current_col.append(grid[row][col])
            
            dic2[convert_to_key(current_col)] += 1

        ans = 0
        for arr in dic:
            ans += dic[arr] * dic2[arr]
        
        return ans
```
```
Given two strings ransomNote and magazine, return true if ransomNote can be constructed by using the letters from magazine and false otherwise.

Each letter in magazine can only be used once in ransomNote.

 

Example 1:

Input: ransomNote = "a", magazine = "b"
Output: false
Example 2:

Input: ransomNote = "aa", magazine = "ab"
Output: false
Example 3:

Input: ransomNote = "aa", magazine = "aab"
Output: true
 

Constraints:

1 <= ransomNote.length, magazine.length <= 105
ransomNote and magazine consist of lowercase English letters.
```
```python
class Solution:
    def canConstruct(self, ransomNote: str, magazine: str) -> bool:
        m = {}
        for letter in magazine:
            if letter in m:
                m[letter]+=1
            else:
                m[letter] =1
        
        for letter in ransomNote:
            if letter in m and m[letter]>0:
                m[letter]-=1
            else:
                return False
        return True
```
```
You're given strings jewels representing the types of stones that are jewels, and stones representing the stones you have. Each character in stones is a type of stone you have. You want to know how many of the stones you have are also jewels.

Letters are case sensitive, so "a" is considered a different type of stone from "A".

 

Example 1:

Input: jewels = "aA", stones = "aAAbbbb"
Output: 3
Example 2:

Input: jewels = "z", stones = "ZZ"
Output: 0
 

Constraints:

1 <= jewels.length, stones.length <= 50
jewels and stones consist of only English letters.
All the characters of jewels are unique.
```
```python
from collections import Counter
class Solution:
    def numJewelsInStones(self, jewels: str, stones: str) -> int:
        s = Counter(stones)
        ans = 0
        for jewel in jewels:
            if jewel in s:
                ans+= s[jewel]
        return ans

```
```
Longest Substring without Repeating Characters

Given a string s, find the length of the longest substring without repeating characters.

 

Example 1:

Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.
Example 2:

Input: s = "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
Example 3:

Input: s = "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.
 

Constraints:

0 <= s.length <= 5 * 104
s consists of English letters, digits, symbols and spaces.
```
```
from collections import defaultdict
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        c = defaultdict(int)
        left = 0
        right = 0
        ans = 0
        for right in range(len(s)):
            
            c[s[right]]+=1
            while c[s[right]]>1:
                c[s[left]]-=1
                left+=1
            ans = max(ans, right - left +1)
        return ans
```