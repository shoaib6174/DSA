# Phone Number Mnemonics

Mnemonics for 1905 are  "1w0j", "1w0k", "1w0l", "1x0j", "1x0k", "1x0l", "1y0j", "1y0k", "1y0l", "1z0j", "1z0k", "1z0l"

#### Digit Representation
```python
DIGIT_LETTERS = {
 "0": ["0"],
 "1": ["1"],
 "2": ["a", "b", "c"],
 "3": ["d", "e", "f"],
 "4": ["g", "h", "i"],
 "5": ["j", "k", "l"],
 "6": ["m", "n", "o"],
 "7": ["p", "q", "r", "s"],
 "8": ["t", "u", "v"],
 "9": ["w", "x", "y", "z"],
}
```
## Approach
- It has some similarity with creating powerset. Here in place of a numeric element, is has multiple options (upto 4). 
- In phone number 9 can be represented by w,x,y,z. Now think about how adding each 9 will change the mnemonic
  - For **9** the mnemonics are- "w" , "x", "y", "Z"
  - For **99** the mnemonics are- "ww", "xw", "yw", "zw", "wx", "xx", "yx", "zx", "wy", "xy", "yy", "zy", "wz", "xz", "yz", "zz"
  - For **999** the mnemonics are -"www", "xww", "yww", "zww", "wxw", "xxw", "yxw", "zxw", "wyw", "xyw", "yyw", "zyw", "wzw", "xzw", "yzw", "zzw", "wwx", "xwx", "ywx", "zwx", "wxx", "xxx", "yxx", "zxx", "wyx", "xyx", "yyx", "zyx", "wzx", "xzx", "yzx", "zzx", "wwy", "xwy", "ywy", "zwy", "wxy", "xxy", "yxy", "zxy", "wyy", "xyy", "yyy", "zyy", "wzy", "xzy", "yzy", "zzy", "wwz", "xwz", "ywz", "zwz", "wxz", "xxz", "yxz", "zxz", "wyz", "xyz", "yyz", "zyz", "wzz", "xzz", "yzz", "zzz"
- To store mnemoics we should use array and convert it to a list at  the end
-  This problem should be solved using recursion


## Recursion 1 ( similar to powerset)
- Input: phoneNumber, idx = None
- idx initialization: if idx is None set idx = len(phoneNumber) - 1
- Base Case: if input idx < 0 then return [ [] ]
- At each iteration-
  - get **mnemonicSoFar** by calling the recursive function using (idx-1)
  - create a new empty list **mnemonics** for storing the mnemonics created by adding letters to members of **mnemonicSoFar**
  - Get the **letters** for the digit of position idx of phoneNumber (  phoneNumber[idx] )
  - Way 1: 
```python
	for letter in letters:
		for subMnemonic in mnemonicSoFar:
			subMnemonic.append(letter)
			mnemonics.append(subMnemonic[:]) # pass a copy of the list
			subMnemonic.pop()
 ```
      
-  
  -  Way 2 :
```python
  for letter in letters:
		for subMnemonic in mnemonicSoFar:
			mnemonics.append(subMnemonic + [letter])
```
  -   
