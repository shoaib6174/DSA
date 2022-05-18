# Min Max Stack
Write a MinMaxStack class for a Min Max
Stack. The class should support:
- Pushing and popping values on and off the stack.
- Peeking at the value at the top of the stack.
- Getting both the minimum and the maximum values in the stack at anygiven point in time.


All class methods, when considered
independently, should run in constant time
and with constant space.

## Approach
- Use both list and dictionary together
  - A list of dictionary where dictionary will contain min and max value for that number {'num': *, 'min':* , 'max':*}
- For pushing an element 
  - Compare it's value with previous (if exists) min and max
  - push it to the stack
- Implement pop
- Implement peek
- Implement getMin
- Implement getMax 


## Solution
```python

class MinMaxStack:
	def __init__(self):
		self.minMaxStack = []
    def peek(self):
        return self.minMaxStack[-1]['num']

    def pop(self):
        return self.minMaxStack.pop()['num']

    def push(self, number):
        newMinMax = {'num': number,
					'min': number,
					'max': number}
		
        if len(self.minMaxStack):
          lastMinMax = self.minMaxStack[-1]
          newMinMax['min'] = min(lastMinMax['min'], number)
          newMinMax['max'] = max(lastMinMax['max'], number)

        self.minMaxStack.append(newMinMax)
			
    def getMin(self):
        
        return self.minMaxStack[-1]['min']

    def getMax(self):
        return self.minMaxStack[-1]['max']

```
