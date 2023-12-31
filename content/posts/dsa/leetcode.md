+++
title = 'Leetcode solutions'
date = 2023-12-30T22:56:49+05:30
draft = false
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

## Problem 3: [Pallindrome](https://leetcode.com/problems/palindrome-number/solutions/)
```py
class Solution(object):
    def isPalindrome(self, x):
        """
        :type x: int
        :rtype: bool
        """
        if x < 0:
            return False
        # Store the number in a variable
        number = x
        # This will store the reverse of the number
        reverse = 0
        while number:
            reverse = reverse * 10 + number % 10
            number //= 10
        return x == reverse
```

## Problem 4: [Longest Common Prefix](https://leetcode.com/problems/longest-common-prefix/)
```py
class Solution(object):
    def longestCommonPrefix(self, strs):
        """
        :type strs: List[str]
        :rtype: str
        """
     
        size = len(strs)
    
        # if size is 0, return empty string
        if (size == 0):
            return ""
    
        if (size == 1):
            return strs[0]
    
        # sort the array of strings
        strs.sort()
        
        # find the minimum length from
        # first and last string
        end = min(len(strs[0]), len(strs[size - 1]))
    
        # find the common prefix between
        # the first and last string
        i = 0
        while (i < end and strs[0][i] == strs[size - 1][i]):
            i += 1
    
        pre = strs[0][0: i]
        return pre
```

## Problem 5: [Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)
```py
class Solution(object):
    def isValid(self, s):
        """
        :type s: str
        :rtype: bool
        """
        # Stack for left symbols
        leftSymbols = []
        # Loop for each character of the string
        for c in s:
            # If left symbol is encountered
            if c in ['(', '{', '[']:
                leftSymbols.append(c)
            # If right symbol is encountered
            elif c == ')' and len(leftSymbols) != 0 and leftSymbols[-1] == '(':
                leftSymbols.pop()
            elif c == '}' and len(leftSymbols) != 0 and leftSymbols[-1] == '{':
                leftSymbols.pop()
            elif c == ']' and len(leftSymbols) != 0 and leftSymbols[-1] == '[':
                leftSymbols.pop()
            # If none of the valid symbols is encountered
            else:
                return False
        return leftSymbols == []
```

## Problem 6: [Largest Substring Between Two Equal Characters](https://leetcode.com/problems/largest-substring-between-two-equal-characters/description/?envType=daily-question&envId=2023-12-31)
```py
class Solution:
    def maxLengthBetweenEqualCharacters(self, s: str) -> int:
        output = -1
        for i in range (0, len(s)):
            for j in range (i+1, len(s)):
                if s[i] == s[j]:
                    output = max(output, j-i-1)
        return output
```