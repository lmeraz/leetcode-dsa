# 02-sliding-window (completed prompts) (anki complete)
## sliding-window-01
What is the general template for a constraint sliding window
https://leetcode.com/explore/interview/card/leetcodes-interview-crash-course-data-structures-and-algorithms/703/arraystrings/4502/
```bash
function fn(arr):
    left = 0
    for (int right = 0; right < arr.length; right++):
        Do some logic to "add" element at arr[right] to window

        while WINDOW_IS_INVALID:
            Do some logic to "remove" element at arr[left] from window
            left++

        Do some logic to update the answer
```
## sliding-window-02
Example 1:
https://leetcode.com/explore/interview/card/leetcodes-interview-crash-course-data-structures-and-algorithms/703/arraystrings/4502/
Given an array of positive integers nums and an integer k, find the length of the longest subarray whose sum is less than or equal to k.
```python
def find_length(nums, k):
    # curr is the current sum of the window
    left = curr = ans = 0
    for right in range(len(nums)):
        curr += nums[right]
        while curr > k:
            curr -= nums[left]
            left += 1
        ans = max(ans, right - left + 1)
    return ans
```
## sliding-window-03
Example 2:
https://leetcode.com/explore/interview/card/leetcodes-interview-crash-course-data-structures-and-algorithms/703/arraystrings/4502/
You are given a binary string s (a string containing only "0" and "1"). You may choose up to one "0" and flip it to a "1". What is the length of the longest substring achievable that contains only "1"?

For example, given s = "1101100111", the answer is 5. If you perform the flip at index 2, the string becomes 1111100111.
```python
# Solution
def find_length(s):
    # curr is the current number of zeros in the window
    left = curr = ans = 0 
    for right in range(len(s)):
        if s[right] == "0":
            curr += 1
        while curr > 1:
            if s[left] == "0":
                curr -= 1
            left += 1
        ans = max(ans, right - left + 1)
    return ans
```
## sliding-window-04
Example 3:
713. Subarray Product Less Than K.
https://leetcode.com/problems/subarray-product-less-than-k/description/

Given an array of positive integers nums and an integer k, return the number of subarrays where the product of all the elements in the subarray is strictly less than k.

Example 1:
Input: nums = [10,5,2,6], k = 100
Output: 8
Explanation: The 8 subarrays that have product less than 100 are:
[10], [5], [2], [6], [10, 5], [5, 2], [2, 6], [5, 2, 6]
Note that [10, 5, 2] is not included as the product of 100 is not strictly less than k.

Example 2:
Input: nums = [1,2,3], k = 0
Output: 0
 
Constraints:
1 <= nums.length <= 3 * 104
1 <= nums[i] <= 1000
0 <= k <= 106
```python
class Solution:
    def numSubarrayProductLessThanK(self, nums: List[int], k: int) -> int:
        if k <= 1:
            return 0
        ans = left = 0
        curr = 1
        for right in range(len(nums)):
            curr *= nums[right]
            while curr >= k:
                curr //= nums[left]
                left += 1
            ans += right - left + 1
        return ans
```
## sliding-window-05
Pseudocode for a fixed window size
https://leetcode.com/explore/interview/card/leetcodes-interview-crash-course-data-structures-and-algorithms/703/arraystrings/4502/
```python
def fixed_window(arr, k):
    curr = # initialize data
    for i in range(k): # iterate to include window values
        # update curr with arr[i] values
    ans = # initialize answer variable
    for i in range(k, len(arr)): # move window
        # include arr[i] to fixed window
        # remove arr[i-k] from fixed window
        # update ans
    return ans
```
## sliding-window-06
Example 4:
https://leetcode.com/explore/interview/card/leetcodes-interview-crash-course-data-structures-and-algorithms/703/arraystrings/4502/
Given an integer array nums and an integer k, find the sum of the subarray with the largest sum whose length is k.
```python
def find_best_subarray(nums, k):
    curr = 0
    for i in range(k):
        curr += nums[i]
    ans = curr
    for i in range(k, len(nums)):
        curr += nums[i] - nums[i - k]
        ans = max(ans, curr)
    return ans
```
## sliding-window-07
643. Maximum Average Subarray 1
https://leetcode.com/problems/maximum-average-subarray-i/description/

You are given an integer array nums consisting of n elements, and an integer k.

Find a contiguous subarray whose length is equal to k that has the maximum average value and return this value. Any answer with a calculation error less than 10-5 will be accepted.

Example 1:
Input: nums = [1,12,-5,-6,50,3], k = 4
Output: 12.75000
Explanation: Maximum average is (12 - 5 - 6 + 50) / 4 = 51 / 4 = 12.75

Example 2:
Input: nums = [5], k = 1
Output: 5.00000

Constraints:
n == nums.length
1 <= k <= n <= 105
-104 <= nums[i] <= 104
```python
class Solution:
    def findMaxAverage(self, nums: List[int], k: int) -> float:
        window_sum= 0
        for i in range(k):
            window_sum+=nums[i]
        max_sum = window_sum
        for i in range(k,len(nums)):
            window_sum+=nums[i]-nums[i-k]
            max_sum = max(max_sum, window_sum)
        return max_sum/k
```
## sliding-window-08
1004. Max Consecutive Ones III
https://leetcode.com/problems/max-consecutive-ones-iii/description/

Given a binary array nums and an integer k, return the maximum number of consecutive 1's in the array if you can flip at most k 0's.

Example 1:
Input: nums = [1,1,1,0,0,0,1,1,1,1,0], k = 2
Output: 6
Explanation: [1,1,1,0,0,1,1,1,1,1,1]
Bolded numbers were flipped from 0 to 1. The longest subarray is underlined.

Example 2:
Input: nums = [0,0,1,1,0,0,1,1,1,0,1,1,0,0,0,1,1,1,1], k = 3
Output: 10
Explanation: [0,0,1,1,1,1,1,1,1,1,1,1,0,0,0,1,1,1,1]
Bolded numbers were flipped from 0 to 1. The longest subarray is underlined.

Constraints:
1 <= nums.length <= 105
nums[i] is either 0 or 1.
0 <= k <= nums.length
```python
class Solution:
    def longestOnes(self, nums: List[int], k: int) -> int:
        left = 0
        zeros = 0
        ans = 0
        for right in range(len(nums)):
            if nums[right]==0:
                zeros+=1
            while zeros>k:
                if nums[left] ==0:
                    zeros-=1
                left+=1
            ans = max(ans,right-left+1)
        return ans
```
## sliding-window-09
209. Minimum Size Subarray Sum
https://leetcode.com/problems/minimum-size-subarray-sum/description/
Given an array of positive integers nums and a positive integer target, return the minimal length of a 
subarray whose sum is greater than or equal to target. If there is no such subarray, return 0 instead.

Example 1:
Input: target = 7, nums = [2,3,1,2,4,3]
Output: 2
Explanation: The subarray [4,3] has the minimal length under the problem constraint.

Example 2:
Input: target = 4, nums = [1,4,4]
Output: 1

Example 3:
Input: target = 11, nums = [1,1,1,1,1,1,1,1]
Output: 0

Constraints:
1 <= target <= 109
1 <= nums.length <= 105
1 <= nums[i] <= 104

Follow up: If you have figured out the O(n) solution, try coding another solution of which the time complexity is O(n log(n)).
```python
class Solution:
    def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        ans = math.inf
        left = 0
        curr = 0
        for right in range(len(nums)):
            curr+=nums[right]
            while curr >= target:
                ans = min(ans, right-left+1)
                curr-=nums[left]
                left+=1
        return ans if ans!= math.inf else 0
```
## sliding-window-10
1456. Maximum Number of Vowels in a Substring of Given Length
https://leetcode.com/problems/maximum-number-of-vowels-in-a-substring-of-given-length/description/

Given a string s and an integer k, return the maximum number of vowel letters in any substring of s with length k.

Vowel letters in English are 'a', 'e', 'i', 'o', and 'u'.

Example 1:
Input: s = "abciiidef", k = 3
Output: 3
Explanation: The substring "iii" contains 3 vowel letters.

Example 2:
Input: s = "aeiou", k = 2
Output: 2
Explanation: Any substring of length 2 contains 2 vowels.

Example 3:
Input: s = "leetcode", k = 3
Output: 2
Explanation: "lee", "eet" and "ode" contain 2 vowels.

Constraints:
1 <= s.length <= 105
s consists of lowercase English letters.
1 <= k <= s.length
```python
class Solution:
    def maxVowels(self, s: str, k: int) -> int:
        ans, curr = 0, 0
        vowels = {'a','e','i','o','u'}
        for i in range(k):
            if s[i] in vowels:
                curr+=1
        ans = curr
        for i in range(k, len(s)):
            if s[i-k] in vowels:
                curr-=1
            if s[i] in vowels:
                curr+=1
            ans = max(ans, curr)
        return ans
```
## sliding-window-11
1208. Get Equal Substring Within Budget
https://leetcode.com/problems/get-equal-substrings-within-budget/description/

You are given two strings s and t of the same length and an integer maxCost.

You want to change s to t. Changing the ith character of s to ith character of t costs |s[i] - t[i]| (i.e., the absolute difference between the ASCII values of the characters).

Return the maximum length of a substring of s that can be changed to be the same as the corresponding substring of t with a cost less than or equal to maxCost. If there is no substring from s that can be changed to its corresponding substring from t, return 0.

Example 1:
Input: s = "abcd", t = "bcdf", maxCost = 3
Output: 3
Explanation: "abc" of s can change to "bcd".
That costs 3, so the maximum length is 3.

Example 2:
Input: s = "abcd", t = "cdef", maxCost = 3
Output: 1
Explanation: Each character in s costs 2 to change to character in t,  so the maximum length is 1.

Example 3:
Input: s = "abcd", t = "acde", maxCost = 0
Output: 1
Explanation: You cannot make any change, so the maximum length is 1.

Constraints:
1 <= s.length <= 105
t.length == s.length
0 <= maxCost <= 106
s and t consist of only lowercase English letters.
```python
class Solution:
    def equalSubstring(self, s: str, t: str, maxCost: int) -> int:
        left = 0
        ans = 0
        curr = 0
        for right in range(len(t)):
            curr += abs(ord(s[right])-ord(t[right]))
            while curr > maxCost:
                curr-=abs(ord(s[left])-ord(t[left]))
                left+=1
            ans = max(ans, right-left+1)
        return ans
```