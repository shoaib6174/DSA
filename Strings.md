# Strings

## Palindrome checkor

#### Algorithm: 
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
## Caesar Cipher Encryptor

#### Algorithm 1:

1. key = key % 26
2. charCode = ord(char) + key
3. if charCode > ord(z) then newChar = chr(ord(a) - 1 + charCode % ord(z))
4. use list to store

```python
def caesarCipherEncryptor(string, key):
    # only lowercase letter
    # O(n) | O(n)
	key = key % 26
	ans = []
	for char in string:
		charCode = ord(char) + key
		newChar = chr(charCode) if charCode <= ord("z") else chr(ord("a") -1 + charCode % ord("z"))
		ans.append(newChar)

    return "".join(ans)

```

#### Algorithm 2:

1. alphabets = sorted list of all characters
2. key = key % 26
3. charCode = alphabets.index(letter) + key
4. newLetter = alphabets[ charCode % 26]

```python
def caesarCipherEncryptor(string, key):
    # only lowercase letter
    # O(n) | O(n)
	key = key % 26
	ans = []
	alphabets = list("abcdefghijklmnopqrstuvwxyz")
    
    for letter in string:
        newLetterCode = alphabets.index(letter) + key 
        # as size of list is fixed(26) so it is a constant time operation
        ans.append(alphabets[newLetterCode % 26])
    return "".join(ans)


```
