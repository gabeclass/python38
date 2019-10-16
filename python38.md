---
title: |
  Python 3.8
author: Henry Schreiner
date: \today
fontsize: 10pt
aspectratio: 169
---


# New in  Python

* Python 3.6
    * Big update
    * First version fast as 2.7
    * New f-strings very popular
* Python 3.7
    * First version faster than 2.7
    * OpenSSL update has affected adoption
* Python 3.8
    * Released just a few days ago!
    * What's new?

# Themes

* Performance
* ABI / Internals
* Static typing

# Python 3.8: Positional-only arguments

## Challenge: write `dict` yourself

```python
d = dict(one=1, two=2)
d = dict({'one':1, 'two':2}
```

. . .

```python
def dict(arg, **kargs):
    ...

dict(arg=3) # OOPS!
```

* You have to use `*args`, and limit to 1 arg yourself. Or...

# Python 3.8: Positional-only arguments

If you look at the signatures of `dict`, `pow`, or some other builtins, you will see something like this:

```python
def dict(arg, /, **kargs):
    ...
```

That is now valid Python in 3.8!

::: div

## Why is it useful?
- Allow kwargs and positional arguments without overlap
- Force positional arguments without names
- You can change the internal name - not part of your API

:::

```python
def f(pos, /, pos_or_kw, *, kw_required, kw_optional=None):
   ...
```

# Python 3.8: Walrus operator

-Assignment in Python is very limited:

```python
item = ...       # Simple
item[...] = ...  # item
item.attr = ...  # attr
a, b, = ...      # tuple
a = b = ...      # chained (special case)
```

But what about assigning in other places, like in the C languages?

```python
if x = True: # Will never be allowed, too easy to make mistake
f(x=True)    # Keyword argument
```

# Python 3.8: Walrus operator (2)

Solution: A new operator!

* Spelling: `:=` (looks like a sideways walrus)
* Works anywhere normal `=` doesn't (one way to do things)
* Often requires parenthesis for clarity

```python
if res := check():
    print(res)
```

* Use carefully, can be powerful
* C++17/C++20 adding variable defines in loops for the same reason

# Python 3.8: f-string debugging

In Python 3.6, f-strings make string interpolation easy:

```python
x = 3
print(f"x = {x}")
```

Debugging is now `DRY` with the `=` specifier:

```python
print(f"{x = }")
```

* Spaces respected
* Mix with complex expressions or formatting

# Python 3.8: Static typing

Static type hints are a big feature of Python 3, and now they are much more powerful:

## Literals type (AKA enums)
```python
def f(val : Literal['yes', 'no', 'auto']): ...
```

## Final (AKA const)
```python
x : Final = True
x = False # Invalid in type checker like mypy
```

## Protocols (ACA C++20 Concepts)
```python
class HasName(Protocol):
    name: str
# Now you can use HasName, will require a name attribute
```


# Other features

* `TypedDict` gives types to dict parts
* `importlib.metadata` gives you info from installed packages (like `importlib.resources`
* `math` and `statistics` have new functions
* `namedtuple`, `pickle`, and more faster
* `list`s use less memory
* `SyntaxError` messages are more detailed in some common cases
* `multiprocessing.shared_memory` - can avoid pickle transfer of objects

# Other developer changes

* `--libs` no longer include `libpython`
* Single ABI for debug/release
* Runtime audit hooks
* New C API for initialization
* Provisional `vectorcall` protocal - fast calling of C functions
* Pickle support out-of-band data (multiple streams) (Protocol 5)
* `__code__` now has `.replace`, like `__signature__`


# Final Words

## Released
* Python.org released
* Docker images released
* Scikit-HEP GCC containers

## Not yet released
* Conda: Coming soon
* Numpy wheels
* Homebrew: In progress
* Still missing in Azure, etc.
* Scikit-HEP build tools (Windows, ManyLinux1 + GCC 9.2)

## Sources
* [Official docs](https://docs.python.org/3.8/whatsnew/3.8.html)
* [RealPython article](https://realpython.com/python38-new-features/)
