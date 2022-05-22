## Python slicing

Python notation `[start:stop:step]` is a wrapper of `slice(start, stop, step)` function.

`slice()` creates a shallow copy.


A few examples

First five elems
```python
nums[:5]
```

Last three
```python
nums[-3:]
```

All but last three
```python
nums[:-2]
```

Every second elem
```python
nums[::2]
```

Reverse list
```python
nums[::-1]
```

Reverse sublist
```python
nums = [1, 2, 3, 4]
print(nums[0:2][::-1])
```

Assigning with slices

New list should match the size of source one. Error otherwise
```python
nums = [1,2,3,4]
nums[::2] = [-1, -3] # [-1, 2, -3, 4]
```

Deletion
```python
nums[0:2]
```
