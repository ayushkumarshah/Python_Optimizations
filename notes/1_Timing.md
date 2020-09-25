# General Tips

- Use real data
- Turn off anti virus
- Have a test suite ready
- Know when to measure

# Measuring time

## Using perf_counter

```python
from time import perf_counter
start = perf_counter()
some_fun()
duration = perf_counter() - start
# gives results in seconds
```

## Using timeit 

For repeatedly executing and measuring the average.

```python
from timeit import timeit
if __name__ == '__main__'
    print('catch', timeit('func_name("argument")', 
          'from __main__ import func_name'))
```

## In IPython

```python
## Loading the functions from external file
%run -n module_name.py
```
-n means not to run main file

```python
%timeit func_name('argument')
```


