# Recursion

### Product Sum

```python
# O(n) | O(depth)
def productSum(array, multiplier = 1):
	sum = 0
    for element in array:
		if type(element) is list:
			sum += productSum(element, multiplier +1)
			
		else:
			sum += element
	
	return sum * multiplier
```

### Permutations
<img width="1106" alt="image" src="https://user-images.githubusercontent.com/40586752/204975324-a0b3b311-021d-423f-aba3-f053e2e6c02a.png">

