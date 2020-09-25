# Tracing memory allocations

Why?
- Data is stored in memory and newly created objects require storage allocation
    which takes time (latency)
- So, memory allocation is important
- Accessing memory is done in layers (CPI, Level 1 cache, Level 2 Cache, Memory,
    SSD / HDD(if extra memory required, memory swapped using page vault) )
- Accessing Level 1 cache is fast (0.5 ns), L2 - 7 ns, Memory - 100 ns, SSD - 16,000 ns


Memory traceback can be done using `tracemalloc`

```python
import tracemalloc
...
...
tracemalloc.start()

## Operations on files (encoding events using json or yaml)
...
...
snapshot = tracemalloc.take_sanpshot()
for stat in snapshot.statistics('lineno')[:10]:
  print(stat)
```

# Memory Profiler

- used for computing memory usage statistics
- @profile decorator used
- Install using `pip install memory_profiler`

## Running

```zsh
python -m memory_profiler module.py
```

## Time based memory profiling

- To see if the memory grows with time.

```zsh
mprof run module.py
mprof plot mprofile_timestamp.dat
```

## IPython

- Check documentation

```python
%load_ext memory_profiler
```

```python
%mprun -f subfun_to_profile function(args)
```
