Permutations of [1,2,3] is [1,2,3] , [1,3,2] , [2,1,3] , [2,3,1] , [3,1,2] and [3,2,1] . 

Numbers of permutations is n!


Algorithom-

- use recursion to solve this problem

Recursion-
- For each position of the input list swap this position's value with each value of the input list

Algorithom
- use position vlaue, input array and an array for storing the permutations as input of the recuresive helper function
- break condition: if the position is equal  to (length of the input array - 1) 
- Break action: add the array to the list of permutations
- for each positon 
   - swap it's vlaue with the value of succeeding positions
   - call the functions for the next position
   - swap back the values

```python
def getPermutations(array):
  permutations = []
	helper(0, array, permutations)
	
	return permutations
	
def helper(i, array, permutations):
	if i == len(array) -1:
		permutations.append(array[:])
	else:
		for j in range(i, len(array)):
			swap(i,j, array)
			helper(i+1, array, permutations)
			swap(i, j, array)
			
def swap(i, j , array):
	array[i], array[j] = array[j], array[i]
		
```
O(n! * n) | O(n! * n)
