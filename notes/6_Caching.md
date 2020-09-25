# Caching

The act of saving computation results and reusing them instead of running the
calculations again. It will speed up the execution but the memory is used to hold 
the results i.e. ``Runtime vs memory trade-off.``

Example of fibonacci sequence program

```python
"""Cachine fibonnaci"""

def fib(n):
    """Return nth fiboacci number"""
    if n < 2:
        return 1
    return fib(n-1) + fib(n-2)


_fib_cache = {}


def fibc(n):
    """Return nth fiboacci number (cached)"""
    if n < 2:
        return 1

    val = _fib_cache.get(n)
    if val is None:
        _fib_cache[n] = val = fibc(n-1) + fibc(n-2)
    return val
 ```

 - 1000 times faster.
 - Take care of caching validation (important)


## Pre-calculating results

Example: Counting number of 1s in a number (binary). Pre-calculate the results.

## LRU Cache

```python
from functools import lru_cache

@lru_cache(maxsize=1024)
def user_from_key(key):
    enc_key = crypt(key, salt)
    return users.get(enc_key)
```

## Joblib

- Keep the computation cache between program runs
- Offers on-disk caching and parallel computing

```zsh
time python module.py
```
