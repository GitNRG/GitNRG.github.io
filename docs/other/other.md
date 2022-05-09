# Other

Dunder methond is the one that starts with "double underscore". For example `__init__`


There is `.toString()` alternative in python.
[Source](https://dbader.org/blog/python-repr-vs-str)

Define the following in class
```python
def __str__(self):
        return f'field_1 is {self.field_1}'
```

Now it could be nicely printed
```python
print(my_car)
str(my_car)
```

The is also `__repr__` dubndler method. Similar one, but slightly different.

Example
```python
class Car:
    def __init__(self, color, mileage):
        self.color = color
        self.mileage = mileage

    def __repr__(self):
        return '__repr__ for Car'

    def __str__(self):
        return '__str__ for Car'


>>> my_car = Car('red', 37281)
>>> print(my_car)
__str__ for Car
>>> '{}'.format(my_car)
'__str__ for Car'
>>> my_car
__repr__ for Car
```

Diff
* The result of the date object’s __str__ function should primarily be readable.
* With __repr__, the idea is that its result should be, above all, unambiguous.

```python
>>> str(today)
'2017-02-02'
>>> repr(today)
'datetime.date(2017, 2, 2)'
```
