# Powerset

Powerset of [1,2,3] is [[], [1], [2], [3], [1, 2], [1, 3], [2, 3], [1, 2, 3]]

## Approach: 
- Think how the powerset changes when a new element is added to the list.
- For [] powerset is [ [] ]
- For [1] powerset is [ []] + [ [1] ]
- For [1 , 2]  powerset is [[], [1]] + [ [2] , [1, 2]]
- For [1,2,3] powerset is [[], [1], [2],  [1, 2] ] + [ [3], [1, 3], [2, 3], [1, 2, 3]]


The problem can be solved using recurrsion and without recurrsion

## Recursion 

### Algorithom 1 ( poping the last element)
- Input: Array
- Base Case: if input is Empty Array return [ [] ]
- At each iteration: 
  - pop the last element of the array and store it
  - get the **subsets** of remaining elements by calling the function on the reduced array
  - add the element to each member of the subset and append it to the **subsets**
  - return the **subsets**

```python
# O(n*2^n) | (n*2^n)
def powerset(array):
	if len(array) == 0:
		return [[]]
	num = [array.pop()]
	subsets = powerset(array)
	for i in range(len(subsets)):
		subsets.append( subsets[i] + num)
	return subsets
```

### Algorithom 2 ( using idx)
- Input: Array and idx=None
- idx initialization: if idx is None set  idx = len(array) - 1 
- Base Case: if input idx < 0 then return [ [] ]
- At each iteration: 
  - get the **subsets**  by calling the function using (idx - 1)
  - add the array[idx] element to each member of the subset and append it to the **subsets**
  - return the **subsets**

```python
def powerset(array, idx =None):
    if idx == None:
		idx = len(array) -1 
	if  idx < 0:
		return [[]]
	subsets = powerset(array, idx-1)
	ele = array[idx]
	for i in range(len(subsets)):
		subsets.append(subsets[i] + [ele])
	return subsets
  ```
  
  ## Without recursion
  Algorithom:
  - set subsets = [ [] ]
  - for each ele of the input array
    - add the ele to all the existing memebers of the subsets list and append them to the subsets

```python
# O(n*2^n) | (n*2^n)
def powerset(array):
	subsets = [[]]
	for ele in array:
		for i in range(len(subsets)):
			subsets.append(subsets[i] + [ele])
	return subsets
```
