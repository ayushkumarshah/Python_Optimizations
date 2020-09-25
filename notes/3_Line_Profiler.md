# Line Profiler

- For finer granularity than just functions i.e. time taken by each line in the
    function
- need to install it  `pip install line_profiler`
- kernprof - command line program
- Use @profile decorator


## Running and viewing
```zsh
kernprof -l module.py
## To view results
python -m line_profiler module.py module.py.lprof
```

## In IPython

```python
%run -n prof.py
```

```python
%load_ext line_profiler
```

```python
%lprun -f subfun_to_profile fun_name(args)
```

