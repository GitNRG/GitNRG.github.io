# Varagrs

To pass variable number of args use `*args`.
Under the hood it's tuple

```python
def x1(*args):
    print("type="+ str(type(args)) + ", len=" + str(len(args)))

x1("a") # type=<class 'tuple'>, len=1
x1(33, 44) # type=<class 'tuple'>, len=2
```

To pass key-value args of variable length use `**kwargs`.
Under the hood it's a dictionary

```python
def x2(**kwargs):
    print("type="+ str(type(kwargs)) + ", len=" + str(len(kwargs)))

x2(k1="v1") # type=<class 'dict'>, len=1
x2(k1=33, k2=44) # type=<class 'dict'>, len=2
```


Both could be used, but args should go first in method declaration.

Name `args` and `kwargs` is just a convention.

Unpacking operators are `*` and `**` before variable name.
They turn a list or a tuple into order method arguments.

For example
```python
def x3(v1, v2):
    print(v1, v2)

var1 = [1, 2]
x3(*var1) # 1 2
x3(*[22, 33]) # 22 33
x3(*(55, 66)) # 55 66

lst1 = [1, 2, 3]
lst2 = [4, 5]
print([*lst1, *lst2]) # [1, 2, 3, 4, 5]
```

The number of args should match exactly (error otherwise).


Similarly maps could be unpacked
```python

def x4(**kwargs):
    print(kwargs)

x4({"a": 1, "b": 2}) # error
x4(**{"a": 1, "b": 2}) # {'a': 1, 'b': 2}


def x5(arg1="hello", arg2="there"):
    print(arg1, arg2)

x5()  # hello there
x5({"arg1": "foo", "arg2": "bar"})  # {'arg1': 'foo', 'arg2': 'bar'} there
dict_args = {"arg1": "foo", "arg2": "bar"}
x5(**dict_args) # foo bar


dict1 = {"k1": "v1", "k2": "v2"}
dict2 = {"k3": "v3"}
print({**dict1, **dict2}) # {'k1': 'v1', 'k2': 'v2', 'k3': 'v3'}
```


String could also be unpacked
```python
print("hello") # hello
print(*"hello") # h e l l o
```
