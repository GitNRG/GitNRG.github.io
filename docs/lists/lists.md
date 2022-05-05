## Python lists

To add all use `extend`
```python
a = [1, 2, 3]
b = [4, 5]
a.extend(b)  # [1, 2, 3, 4, 5]
```

Sort list with custom comparator
```python
from functools import cmp_to_key

def compare(a, b):
    return a - b

sorted([8, 5, 12], key=cmp_to_key(compare))
````

Nice way to init list
```python
lst = [33] * 3 # [33, 33, 33]
```
