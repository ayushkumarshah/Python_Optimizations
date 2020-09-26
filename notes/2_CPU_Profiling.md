# CPU Profiling

- cProfile (deterministic profiler) recommended
- Deterministic profilers record every function call, return, and exception.
- Statistical profilers record where the program is at small intervals.
- pstats to display profiler generated statistics file

## Running cProfiler

### Whole file

```zsh
python -m cProfile module.py
```

### Portion of file

Add the line in code:

```python
if __name__ == '__main__':
    ...
    # where profiler needed
    import cProfile
    cProfile.run('fun_name(cases)')
    ## OR
    cProfile.run('fun_name(cases)', filename='prof.out or program.prof')
```

Then run the module

```zsh
python module.py
```

In notebook

```python
## Importing functions from the module
%run -n module.py
```

```python
%prun fun_name(args)
## OR
%prun -D program.prof fun_name(args)

## For more info about prun
%prun?

## Sorting
%prun -s cumulative fun_name(args)
```

### Snakeviz

```zsh
snakeviz prof.out/program.prof
```

In notebook

```python
%load_ext sankeviz
```

For single line code:

```python
% sankeviz fun_name(args)
```

For multiple lines code:

```python
%%snakeviz
# code here
# ....
# ...
```

**Note: cProfile slows down the program. Other lightweight statistical Profilers 
like: vn_prof package**
