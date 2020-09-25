# Parallel Computing

- Parallelism vs Concurrency
  - Concurrency: dealing with lots of things at once.
  - Parallelism: doing lots of things at once.
- Amdahl's Law : formula which gives theoretical limits of speed increase or
    latency as a result of parallel computing.
  $$S(N) = \frac{1}{(1-P) + \frac{P}{N}}$$

## I/O Bound vs CPU Bound

- I/O Bound programs - spend time in input/output such as network or disk and 
- CPU Bound Programs - spend time in calculations

Python provides 3 options for parallelism or concurrency: 
- Threads - independent units of execution that share the same memory space.
    Global variables are visible to all threads. Great for IO bound but not for
    CPU bound (due to GIL: CPython can use only one core from the CPU)
- processes - independent units of execution that have different memory space.
    Using multiple processes, you can use multiple cores, hence great for CPU
    bound programs. However, no communication between processes is expensive
    since memory is not shared. So, data needs to be serialized, send it over
    socket/pipe and deserialize it on the other side.
- asyncio - handle a lot of connections. uses a single thread to listen to all
    connections.

## Summary of usage

![summary](images/summary.png)

## Threads

Example: Getting user info of many users in parallel from GitHub.

First, code normally and analyze using timeit and profiler. If CPU time is very 
less than the Wall Time and most time being spent in
socket operations, then threading will improve the time.

```python
"""Thread Pool Example"""

from collections import namedtuple
from concurrent.futures import ThreadPoolExecutor
from datetime import datetime
from urllib.request import urlopen
import json

User = namedtuple('User', 'login name joined')


def user_info(login):
    """Get user information from github"""
    fp = urlopen('https://api.github.com/users/{}'.format(login))
    reply = json.load(fp)

    joined = datetime.strptime(reply['created_at'], '%Y-%m-%dT%H:%M:%SZ')
    return User(login, reply['name'], joined)


def users_info(logins):
    """Get user information for several users"""
    return [user_info(login) for login in logins]


def users_info_thr(logins):
    """Get user information for several users - using thread pool"""
    with ThreadPoolExecutor() as pool:
        return list(pool.map(user_info, logins))


if __name__ == '__main__':
    logins = [
        'gvanrossum',
        'wesm',
        'tebeka',
        'torvalds',
    ]
```

## Processes

Example: Decompressing data

First, code normally and analyze using timeit and profiler. If CPU time is
almost same as the Wall Time and most time being spent in
computations, then processes will improve the time.

```python
"""Process pool example"""
from concurrent.futures import ProcessPoolExecutor
import bz2


def unpack(requests):
    """Unpack a list of requests compressed in bz2"""
    return [bz2.decompress(request) for request in requests]


def unpack_proc(requests):
    """Unpack a list of requests compressed in bz2 using a process pool"""
    # Default to numbers of cores
    with ProcessPoolExecutor() as pool:
        return list(pool.map(bz2.decompress, requests))


if __name__ == '__main__':
    with open('huck-finn.txt', 'rb') as fp:
        data = fp.read()

    bz2data = bz2.compress(data)
    print(len(bz2data) / len(data))  # About 27%
    print(bz2.decompress(bz2data) == data)  # Loseless

    requests = [bz2data] * 300

```

## Asyncio

See example code
