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


