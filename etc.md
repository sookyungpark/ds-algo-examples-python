## Map to Sorted List
```python
sorted_list = sorted(myDict.items(), key=lambda x: x[0])
```

## Object ID
```python
objectId = id(obj)
```

## Filter None Item from list
```python
str_list = list(filter(None, str_list))
```

## Get Maximum value
```python
from functools import reduce
reduce(lambda a,b: a if a > b else b ,li)
```

## Using Next
```python
myList = [0.0 , 0.0, 0.0, 2.0, 2.0]
result = next((i for i, x in enumerate(myList) if x), None) # x!= 0 for strict match
# result == 3
```

## Joining Integer Array to String
```python
num_list = [-1, 0, 1, 3, 4, 5, 9]
print(" ".join(map(str, num_list)))
```

## Joining Integer Array to String
```python
num_list = [-1, 0, 1, 3, 4, 5, 9]
print(" ".join(map(str, num_list)))
```

## Using Sum for conditional sum
```python
sum(x == True for x in sieve)
```

## Check if number is perfect square
```python
root = math.sqrt(number)
int(root + 0.5) ** 2 == number
```
0.5 is for float square ambiguity when number is big enough

## Prime find with yield
```python
def prime_gen():
    n = 2
    primes = []
    while True:
        if any((n % k) == 0 for k in primes):
            n += 1
            continue
        primes.append(n)
        yield n
```

## Prime Factors
```python
def prime_factors(n):
    for i in itertools.chain([2], itertools.count(3, 2)):
        if n <= 1:
            break
        while n % i == 0:
            n //= i
            yield i
```
