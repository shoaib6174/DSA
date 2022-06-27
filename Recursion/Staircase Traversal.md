# Staircase Traversal
You're given two positive integers representing the height of a staircase and the maximum number of steps
that you can advance up the staircase at a time. Write a function that returns the number of ways in which
you can climb the staircase. For example, if you were given a staircase of **height = 3** and **maxSteps = 2** 
you could climb the staircase in 3 ways. 
You could take 1 step, 1 step, then 1 step,
you could also take 1 step, then 2steps, 
and you could take 2 steps, then 1 step. Note that **maxSteps <= height** will always be true.

#### Sample Input
height = 4

maxSteps = 2
#### Sample Output
5

You can climb the staircase in the following ways:
- 1, 1, 1, 1
- 1, 1, 2
- 1, 2, 1
- 2, 1, 1
- 2, 2

## Approach

- ways(n) = ways(n-1) + ways(n-2) + .........+ ways(n-maxSteps) 
- For maxSteps = 3
  - ways(n) =   ways(n-1) + ways(n-2) + ways(n-3)

## Solution 1
- Use recurrsion

- Recurrsion
  - input: height, maxSteps
  - base case: if height == 0: return 1
  - NumberofWays = ways(height-1) + ways(height-2) + .........+ ways(n-maxSteps) 
  - return NumberofWays
```python
# O( height ^ maxSteps) | O(height)
def staircaseTraversal(height, maxSteps):
	if height == 0:
		return 1
	numberofWays = 0
	
	# for step in range(1,  maxSteps +1):
	# 	if height - step >=0:
	# 		numberofWays+= helper(height-step, maxSteps)
	
	for step in range(1, min(height, maxSteps) +1):
		numberofWays+= staircaseTraversal(height-step, maxSteps)
			
	return numberofWays
```

## Solution 2
- Use memomization

```python
# O(n*k) | O(n)
def staircaseTraversal(height, maxSteps):
	return staircaseTraversalHelper(height, maxSteps, {0: 1, 1:1})

def staircaseTraversalHelper(height, maxSteps, memo):
	if height not in memo:
		numberofWays = 0
		for step in range(1, min(height, maxSteps) +1):
			numberofWays+= staircaseTraversalHelper(height-step, maxSteps, memo)

		memo[height] = numberofWays
	return memo[height]
```

## Solution 3
- use dynamic programming

```python
#O(n*k) | O(n)
def staircaseTraversal(height, maxSteps):
	ways = [0] * (height +1)
	ways[0] = 1
	
	
	for i in range(1, height+1):
		for k in range(1, maxSteps+1):
			ways[i] += ways[i-k] 
	
	return ways[height]
```

## Solution 4

- optimize the previous solution by keeping track of running sum and leaving var

```python
def staircaseTraversal(height, maxSteps):
	ways = [0] * (height +1)
	ways[0] = 1

	runningSum = 1
	for i in range(1, height+1):
		ways[i] = runningSum
		runningSum += ways[i] -ways[i-maxSteps]

	return ways[height]
  
  ```
