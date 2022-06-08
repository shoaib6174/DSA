# Strings

## Palindrome check

Algorithom: 
1. Declare left and right pointer
2. while left < right
3. If char at pointers are not same then return false
4. If same then go to next character

```python

def isPalindrome(string):
    # two pointers from two sides. O(N)| O(1)
    left = 0
	right = len(string) - 1
	
	while left <= right:
		if not string[left] == string[right]:
			return False
		else:
			left += 1
			right -= 1
			
	return True
```
