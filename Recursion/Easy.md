# Nth Fibonacci

#### Approach 1:
- Use recurrsion 
- O(2^n) | O(n)

```python

def getNthFib(n):
    if n == 1:
      return 0
    elif n == 2:
      return 1
     else:
      return getNthFib(n-1) + getNthFib(n-2)

```

#### Approach 2:
- Use memomization
- its a top down approach
- O(n) | O(n)

```python

def getNthFib(n, memo = {1: 0, 2: 1}):
  if n in memo:
    return memo[n]
  else:
    memo[n] =  getNthFib(n-1, memo) + getNthFib(n-2, memo)
    return memo[n]
```

#### Approach 3
- Use tabulation
- it's a bottom up apprach
- O(n) | O(n)
- Though the complexity is same as memomization but it will be faster because it doesn;t have many recursive calls and return statements


```python

def getNthFib(n):
  fibs = [0] * (n+1)
  fibs[0] = 1 #It will work as seed to make fibs[2] = 1
  
  counter = 2
    
  while counter <= n:
    fibs[counter] = fibs[counter -1] + fibs[counter - 2]
    counter += 1
  
  return fibs[n] 
```

#### Approach 4:
- store the last two elements
- run a while loop upto N
- at each iteration change the last two elements
- O(n) | O(1)

``` python
def getNthFib(n):
  last = 1
  secondLast = 0
  
  counter = 3
  while counter <= n:
    last, secondLast = last + secondLast, last
    counter += 1
    
  return last if n > 1 else 0
```
