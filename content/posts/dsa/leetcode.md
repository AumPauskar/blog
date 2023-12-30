+++
title = 'Leetcode solutions'
date = 2023-12-30T22:56:49+05:30
draft = true
+++

# Leetcode solutions
## Problem 1: [Two Sum](https://leetcode.com/problems/two-sum/description/)
```py
class Solution(object):
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        for i in range(0, len(nums)):
            for j in range(0, len(nums)):
                if nums[i]+nums[j] == target and i!=j:
                    op = [i,j]
                    return op
```

## Problem 2: [Roman to integer](https://leetcode.com/problems/roman-to-integer/)
```py
class Solution(object):
    def romanToInt(self, s):
        """
        :type s: str
        :rtype: int
        """
        roman = {'I':1,'V':5,'X':10,'L':50,'C':100,'D':500,'M':1000,'IV':4,'IX':9,'XL':40,'XC':90,'CD':400,'CM':900}
        i = 0
        num = 0
        while i < len(s):
            if i+1<len(s) and s[i:i+2] in roman:
                num+=roman[s[i:i+2]]
                i+=2
            else:
                #print(i)
                num+=roman[s[i]]
                i+=1
        return num
```
