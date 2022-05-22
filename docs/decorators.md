# Decorators

Decorators are simply method wrappers.
They get method as an argument and return method execution result, but can add arbitrary logic around.


[Long read article](https://realpython.com/primer-on-python-decorators/)

Brief notes below

This is a code without wrapper

```python
def a(arg):
    return "a" + arg

def b(arg):
    return "b" + arg

def c(my_func):
    return my_func("x")

print(c(a)) # ax
print(c(b)) # bx
```


This is a code with decorator
```python
def my_decorator(func):
    def wrapper():
        print("This happens before execution")
        func()
        print("This happens after execution")
    return wrapper


@my_decorator
def say_one():
    print("one")

say_one()
```

It prints
```
This happens before execution
one
This happens after execution
```


Decorators may also return values just like any other method
```python
def inc(func):
    def wrapper():
        return func() + 1
    return wrapper

@inc
def get_one():
    return 1

print(get_one()) # prints 2
```


To pass arguments - use args & kwargs

```python
def square(func):
    def wrapper(*args, **kwargs):
        return func(*args, **kwargs)**2  # note, args are unpacked
    return wrapper


@square
def pick_first(*args):
    return args[0]


print(pick_first(2))  # 4
print(pick_first(4, 2))  # 16
print(pick_first(6, 4, 2))  # 36
```


Decorator may also decorate the whole class.
Basically it's just constructor decorator

```python
def class_dec(cls):
    def wrapper(*args, **kwargs):
        print("Injected line")
        return cls(*args, **kwargs)
    return wrapper

@class_dec
class Helper:
    def __init__(self, value):
        print("Init")
        self.value = value

    def print_value(self):
        print(self.value)


helper = Helper(33)  # prints "Injected line" and "Init"
helper.print_value()  # prints just "33" because decorator not used
```


Decorator could be nested
```python
def outer(func):
    def wrapper():
        print("Outer")
        func()
    return wrapper

def inner(func):
    def wrapper():
        print("Inner")
        func()
    return wrapper

@outer
@inner
def hello():
    print("Hello")

hello()
```

prints
```
Outer
Inner
Hello
```


It's possible to pass args to decorators. Simply wrap decorator method with another one that accepts necessary argument & use them under the hood.

```python
def repeat_str(num):
    def repeat_str_decorator(func):
        def wrapper():
            return func() * num
        return wrapper
    return repeat_str_decorator

@repeat_str(num=1)
def say_boo_once():
    return "Boo"

@repeat_str(num=2)
def say_boo_twice():
    return "Boo"

print(say_boo_once())  # Boo
print(say_boo_twice())  # BooBoo
```



There are 2 ways to store decorator state
1) In method attributes (probably not the best choice)
2) In a class

In case of method attributes
```python
def count_calls(func):
    def wrapper():
        wrapper.num_calls += 1
        print("Num calls " + str(wrapper.num_calls))
        func()
    wrapper.num_calls = 0
    return wrapper

@count_calls
def say_boo():
    print("Boo")

say_boo()
say_boo()
```

prints

```
Num calls 1
Boo
Num calls 2
Boo
```


In case of class counter the special `__call__` method is required. It allows calling instance of class right away. For decorator all we need is a `func` in constructor

```python
class CountCalls:
    def __init__(self, func):
        self.func = func
        self.num_calls = 0

    def __call__(self, *args, **kwargs):
        self.num_calls += 1
        print(f"Call {self.num_calls} of {self.func.__name__!r}")
        return self.func(*args, **kwargs)


@CountCalls
def say_whee():
    print("Whee!")

say_whee()
say_whee()
```

prints
```
Call 1 of 'say_whee'
Whee!
Call 2 of 'say_whee'
Whee!
```
