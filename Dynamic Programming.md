# Dynamic Programming

List by Love Babbar: https://whimsical.com/dp-sheet-by-love-babbar-EELKgSMWg51ypLyfn9mTjr

## 1. Max Subset sum no adjacent

Given an array arr[] of positive numbers, The task is to find the maximum sum of a subsequence such that no 2 numbers in the sequence should be adjacent in the array.

```
Input: arr[] = {5, 5, 10, 100, 10, 5}
Output: 110
Explanation: Pick the subsequence {5, 100, 5}.
```

Solution:
1. Return max if len()<= 2
2. for a maxsum array, for each element from 3rd, set value to max( arr[i] + arr[i-2], arr[i-i]) 
3. initialize by coppying array
4. return last element

``` python

# O(n) | O(n)
# the maximum at each point starting from 2nd position

def maxSubsetSumNoAdjacent(array):
    # create a newArray -> maxSums
    # maxSums[i] = max(maxSums[i-1], maxSums[i-2] + array[i])

    # corner cases
    if len(array) == 0:
        return 0
    elif len(array) <= 2:
        return max(array)

    maxSums = array[:]  # copy

    maxSums[1] = max(array[0], array[1])  #the max in the 2nd position
    for i in range(2, len(array)):
        maxSums[i] = max(maxSums[i-1], maxSums[i-2] + array[i])

    return maxSums[-1]

```

* Track maxmimum possilbe value including the value of current position using prev and two_prev
* Return the max of prev and two_prev


```python

# O(n) | O(1)
# currSum is maximum of including the current value ( not max of the whole sequence)
# use prev and two_prev so carry to values of two options and return the max at the end
# currSum is curr added with  n-2 or n-3

def maxSubsetSumNoAdjacent(array):

	l =len(array)
	if l == 0:
		return 0
	elif l < 2:
		return max(array)
	
	two_prev = array[0]
	prev = array[1]
	currSum = 0
	
	for i in range(2, l):

        # currSum = (n-2) + curr or (n-3) + curr
        # prev - array[i-1] gives (n-3)
        
		currSum = array[i] + max( prev - array[i-1], two_prev)
		
		two_prev = prev
		prev = currSum
		
		
	return max(prev, two_prev)

```


## 2. Number of ways to make change

Solution: for each coin, for each ammount add how many ways to make [ammount - coin]

``` python
# O(nd) | O(n)
# for each coin: for (coin to n) ammount:  ways[ammount] = ways[ammount - coin]
# start with ways[0] = 1

def numberOfWaysToMakeChange(n, denoms):
    ways = [0] * (n+1)
	ways[0] = 1
	for denom in denoms:
		for ammount in range(1, n+1):
			if denom <= ammount:
				ways[ammount] += ways[ammount - denom]
				
	return ways[n]

```

## 3. Min number of coins to make changes


Solution: for each coin, for each ammount, minCoins is current one or "minCoins(ammoun-coin) plus 1" 

```python
# For each coin, For each ammount, #minCoins[ammount] = min( minCoins[ammount- coin] + 1 , minCoins[ammount])
# initialize minCoins at float("inf")
# O(nd) | O(n)
def minNumberOfCoinsForChange(n, denoms):
    minCoins = [float("inf")] * (n+1)
    minCoins[0] = 0
    
    for denom in denoms:
        for ammount in range(denom, n+1):
            minCoins[ammount] = min(minCoins[ammount - denom] + 1, minCoins[ammount])
    
    return minCoins[-1] if minCoins[-1] <= n else -1

```

## 4. Levenshtein Distance

Problem: Min operations (add, remove, substitute) on string1 to get string2

![image](https://user-images.githubusercontent.com/40586752/203989017-f9d0b47d-58c7-412a-886c-4d8920f6e572.png)

![image](https://user-images.githubusercontent.com/40586752/203989316-e1c3dd1d-16a4-4120-82a2-8ba9f9b4b79b.png)

Sol: 
* create 2d matrix including empty cell and fill first col and row
* if str1[i] and str2[j] matches then value of prev cell in row (distance[i-1][j-1]) 
* else: min of sorrounding 3 cells + 1

```python
# 2D array 
# target string's character in col
# given string in row
# if str1[r] == str2[r] : E[r][c] = E[r-1][c-1] ## prev in row
# else: E[r][c] = 1 + min of sorrudings 3 cells
def levenshteinDistance(str1, str2):
    edits = [[0 for _ in range(len(str2)+1)] for _ in range(len(str1) +1)]

    # first row 1 to len(str2)
    for i in range(len(str2)+1):
        edits[0][i] = i
    # first col 1 to len(str1)
    for i in range(len(str1)+1):
        edits[i][0]  = i

    for i in range(1,len(str1) + 1):
        for j in range(1,len(str2) +1):
            if str1[i - 1] == str2[j - 1]:
                edits[i][j] = edits[i-1][j-1]
            else:
                edits[i][j] = 1 + min(edits[i-1][j-1], edits[i-1][j], edits[i][j-1])
    
            
    # print(edits)
    return edits[-1][-1]

```

## 5. Max Sum increasing subsequence

Problem: Return max sum and subsequnce

Solution:
1. copy the array (sums)
2. at each index of sums, store the max sum that can be generated using a increasing subsequence ending at that index's sum
3. In another list initialized with None, at each index, store the positon of prev element of the subSeq which gave the max 
4. Build the seq using idx of maxSum

```python
# O(n^2) | O(n)
def maxSumIncreasingSubsequence(array):
    sums = array[:]
    prevPosition = [None for _ in range(len(array))]
    maxSumIdx = 0

    for i in range(len(array)):
        currNum = array[i]
        for prev in range(i):
            otherNum = array[prev]
            if otherNum < currNum:
                if sums[prev] + currNum > sums[i]:
                    sums[i] = sums[prev] + currNum
                    prevPosition[i] = prev
        if sums[i] > sums[maxSumIdx]:
            maxSumIdx = i

    # max sum of sub sequence
    maxSum = sums[maxSumIdx]

    # building the sequence
    seq = []
    while maxSumIdx is not None:
        seq.append(array[maxSumIdx])
        maxSumIdx = prevPosition[maxSumIdx]
        
    seq = list(reversed(seq))

    return [maxSum, seq]

```

