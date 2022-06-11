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

## Run-length encoding

- use counter and increase count if current mathes with previous
- if counter exceeds 9 or leters doesn't match then apeend counter and letter to a list
- when the for ends, entry the current current and letter to the list

```python
def runLengthEncoding(string):
    # O(n) | O(n)
    result = []
    counter = 1
    previous = string[0]

    for letter in string[1:]:
        if letter == previous and counter < 9:
            counter += 1
        else:
            result.append(str(counter))
            result.append(previous)

            previous = letter
            counter = 1
            
    result.append(f"{counter}{previous}")
    return "".join(result)
            
```

## Generate Document

- count frequency of the letters of characters string and store it in a dictionary
- for each letter in document 
	- if the letter is not in frequency dict or freqency is 0 then return Flse
	- ohterwise decreace frequency count of characters string by 1 
- return True

```python
def generateDocument(characters, document):
    # O(m+n) | O(c)
    charFreq = counter(characters)

    for k in document:
        if k not in charFreq or charFreq[k] == 0:
            return False
        charFreq[k] -= 1
    
    return True


def counter(string):
    freq = {}
    
    for letter in string:
        freq[letter] = freq[letter] + 1 if letter in freq else 1
        
    return freq
```


## First non-repeating character
- make a frequency dictionary from the characters of the string 
- iterate the string and return the first positon for which the frequency is 1

```python
def firstNonRepeatingCharacter(string):
    # O(n) | O(1) because the string only contains lowercase charecters
	freq = {}
	
	for c in string:
		freq[c] = freq[c] + 1 if c in freq else 1
	for i in range(len(string)):
		if freq[string[i]] == 1:
			return i
    return -1
```

## Longest Palindromic Substring
