# Three Number Sort

You're given an array of integers and another array of
three distinct integers. The first array is guaranteed to
only contain integers that are in the second array, and the
second array represents a desired order for the integers
in the first array. For example, a second array of
[x, y, z] represents a desired order of
[x, x, ..., x, y, y, ..., y, z, z, ..., z]
in the first array.

Write a function that sorts the first array according to the
desired order in the second array.


The function should perform this in place (i.e., it should
mutate the input array), and it shouldn't use any auxiliary
space (i.e., it should run with constant space: O(1)
space).


Note that the desired order won't necessarily be
ascending or descending and that the first array won't
necessarily contain all three integers found in the second
array—it might only contain one or two.


**Sample Input**
```
array = [1, 0, 0, -1, -1, 0, 1, 1]
order = [0, 1, -1]
```

**Sample Output**
```
[0, 0, 0, 1, 1, 1, -1, -1]
```

Similar problem- https://leetcode.com/problems/sort-colors/
## Approach
- This problem is simmilar to [Dutch national flag problem](https://en.wikipedia.org/wiki/Dutch_national_flag_problem) algorithm
- Iterate through the list
  - use 3 pointer
  - use the secondIdx to iterate the list
  - if value is equal to firstValue then swap with the position of first pointer. Increase firstIdx and secondIdx
  - if value is equal to thirtdValue then swap with the position of third pointer and thirdIdx -= 1 It sends the value from end of the list to the position of secondIdx. So iterating untill secondIdx <= thridIdx is enough
  - if value is equal to secondValue then secondIdx +=1


## Solution 
```python
def threeNumberSort(array, order):
	# O(N) | O(1)
    firstIdx = 0
	secondIdx = 0
	thirdIdx = len(array) -1
	
	
	firstValue = order[0]
	secondValue = order[1]
	
	while secondIdx <= thirdIdx:
		current = array[secondIdx]
		
		if current == firstValue:
			array[firstIdx] , array[secondIdx] = array[secondIdx] , array[firstIdx]
			firstIdx += 1
			secondIdx += 1
		elif current == secondValue:
			secondIdx += 1
		else:
			array[thirdIdx] , array[secondIdx] = array[secondIdx] , array[thirdIdx]
			thirdIdx -= 1
		
	return array
```
