# Strings

## Palindrome checker
https://leetcode.com/problems/valid-palindrome/

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
https://www.hackerrank.com/challenges/caesar-cipher-1/problem


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

Store all the possible values in a list. For each character add the key with the index of the character then modulus is length of list.
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

https://leetcode.com/problems/string-compression/

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

https://leetcode.com/problems/ransom-note/

You're given a string of available characters and a string representing a document that you need to
generate. Write a function that determines if you can generate the document using the available
characters. If you can generate the document, your function should return true ; otherwise, it should
return false .


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
	
	# freq[letter] = freq.get(letter, 0) + 1
    # freq = collections.Counter(s)
        
    return freq
```


## First non-repeating character

https://leetcode.com/problems/first-unique-character-in-a-string/
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
https://leetcode.com/problems/longest-palindromic-substring/

#### Approach 1:
- Generate all the substring
- if panlindromic then take length and compare with current maximum


```python
def longestPalindromicSubstring(string):
    #O(n^3) ! O(n)
    longest = string[0]
    
    for i in range(len(string) -1):
        for j in range(len(string) , i+1, -1):
            subString = string[i:j]
            longest = subString if palindromeLength(subString) > len(longest) else longest
    return longest

    
def palindromeLength(s):
    left = 0
    right = len(s) - 1

    while left < right:
        if s[left] != s[right]:
            return 0
        left += 1
        right -= 1
        
    return len(s)
 ```

#### Approach 2:

- consider each element from index 1 of the string as center of palindrome
	- find the length of palindrome for even length paliondrome and odd length palindrome centering this element
	- compare the maximum of these lengthd to the current maximum
	- don't forget to store the start and end position

```python
def longestPalindromicSubstring(string):
    # O(n^2) | O(n)
    pos = [0,1]
    for i in range(1, len(string)):
            oddLenPalinPos = palindromePosition(string, i-1, i+1)
            evenLenPalinPos = palindromePosition(string, i-1, i)
            
            maxLen = max(oddLenPalinPos, evenLenPalinPos, key = lambda x: x[1] - x[0])
            pos = max(maxLen, pos, key= lambda x: x[1] -x[0])
            
    return string[pos[0]:pos[1]]
            
def palindromePosition(string, left, right):
    while left >= 0 and right < len(string):
        if string[left] != string[right]:
            break    
        left-=1
        right += 1
        
    return [left+1, right]
```

## Group Anagrams
https://leetcode.com/problems/group-anagrams/

#### Approach:

- declare a dictionary to store the anagrams
- use sorted word as key of the dict as anagram will have same sorted string. like- sorted form of "dcba"  and "cdba" both is "abcd"
- iterate through the words and add them to the list associated to the sorted word

```python
def groupAnagrams(words):
    # O( numOfWords * sizeOfLongestWord * log(sizeOfLongestWord)) | O(numOfWords * sizeOfLongestWord)
    anagrams = {}

    for word in words:
        sortedWord = "".join(sorted(word))
        if sortedWord not in anagrams:
            anagrams[sortedWord] = []
            
        anagrams[sortedWord].append(word)
    
    return list(anagrams.values())
```

## Restore IP Addrresses
https://leetcode.com/problems/restore-ip-addresses/

#### Approach
- use a function to verify if a subString/integer is valid
- Use 3 for loops to iterate over the string 
- Use declared list ["" , "", "", ''] instead of appedning  
- Run the for loop for minimum of next 3 character and  length of string so avoid empty string

``` python
def validIPAddresses(string):
    # O(1) | O(1) becasue max length of string is fixed
    ips = []
    for i in range(1, min(4, len(string))) : 
        currIP = ["" , "", "", '']
        currIP[0] = string[:i]
        if not isValid(currIP[0]):
            continue
        
        for j in range(i+1, i + min(4, len(string)-i) ):
            currIP[1] = string[i:j]
            if not isValid(currIP[1]):
                continue

            for k in range(j+1, j + min(4, len(string)- j) ):
                currIP[2] = string[j:k]
                currIP[3] = string[k:]

                if isValid(currIP[2]) and isValid(currIP[3]):
                    ips.append(".".join(currIP))
                
    return ips

def isValid(subString):
    ssInt = int(subString)
    if len(subString) == 0 or int(subString) > 255 :
        return False
    if len(subString) > 1 and subString[0] == "0":
        return False
    return True
```


## Reverse Words in a String
https://leetcode.com/problems/reverse-words-in-a-string/

#### Approach 1
- use loop to find whitespace and add the previous word  to list using sliding window
- if white space then 
	- add the word between slow and fast in the ans list	 
	- reset both pointer
	- add it to the ans list
- if not whitespace increase the fast pointer
- use while loop till fast is less then 0
- at the end of the while loop add the word between slow and fast in the ans list	

```python
def reverseWordsInString(string):
    # O(n) | O(n)
    ans = []
    slow = len(string)
    fast = slow - 1

    while fast >= 0:
        if string[fast] == " ":
            ans.append(string[fast+1:slow] + " " )
            slow  = fast
        fast -= 1

    ans.append(string[fast+1:slow])

    return "".join(ans)
```

##### Another code

```python
def reverseWordsInString(string):
    # O(n) | O(n)
    endOfTheWord = len(string)
    words = []
    for i in range(len(string)-1, -1, -1):
        if string[i] == " ":
            words.append(string[i+1:endOfTheWord])
            endOfTheWord = i
            
    words.append(string[:endOfTheWord])

    return " ".join(words)
```
## Minimum Characters for words

Write a function that takes in an array of words and returns the smallest array of characters needed to
form all of the words. The characters don't need to be in any particular order.
For example, the characters ["y", "r", "o", "u"] are needed to form the words
["your", "you", "or", "yo"] .
Note: the input words won't contain any spaces; however, they might contain punctuation and/or special
characters.
``` Python
Input_Words = ["this", "that", "did", "deed", "them!", "a"]

Output = ["t", "t", "h", "i", "s", "a", "d", "d", "e", "e", "m", "!"]
```

#### Approach
- dictionary for storing character frequency
- count the frequency for each word
- update the character frequency
- make a list from the character frequency dictionary

```python
def minimumCharactersForWords(words):
    # w = num of words, l = max length of word, c = numbero of unique characters
    # time:  O(wl + c). but c < wl. so O(wl)
    # space: O(c)
    characters = {}
    for word in words:
        wordFreq = countCharacters(word)
        updateMaxFreqOfCharacters(wordFreq, characters)
    
    ans = []
    for c , value in characters.items():
        for _ in range(value):
            ans.append(c)

    return ans
    
def countCharacters(s):
    freq = {}
    for c in s:
        if c not in freq:
            freq[c] = 0
        freq[c] += 1

    return freq

def updateMaxFreqOfCharacters(wordFreq, characterFreq):
    for c in wordFreq:
        freq = wordFreq[c]
        if c in characterFreq:
            characterFreq[c] = max(freq, characterFreq[c])
        else:
            characterFreq[c] = freq
    return characterFreq

```
