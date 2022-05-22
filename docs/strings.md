# Strings

There are two types of strings in Python
* byte string (used in python 2)
* unicode strings (python 3)

By default unicode string is used. Unicode is implemented as UTF-8 by default.

To defined byte string use "b" prefix. Use no prefix or "u" for unicode
```python
b"abc"
u"abc"
"abc"
```

There are also raw strings prefixed with "r"
```python
r"abc\nxyz"
```
This text doesn't **not** contain new line


The are also format string that can evaluate expressions
```python
b = 'bar'
s = f'foo{b}'
```
Inside expression any valid Python expression can be used, including function and method calls.
