# Tips for optimization

- Pick the right data structure (dequeu, heap, PriorityQueue, bisect)
- Local caching of names

  To check how python compiles a function:

  ```python
  import dis
  dis.dis(fun_name)
  ```

  Global look up takes more time. So, save a local copy in the local function. 

- Remove function calls (TANSTAAFL) since function call increases time. So, find
    trade off between structure and time cost. Use inline function if possible.
- Don't use property (setter and getter) unless necessary. Since propert is
    almost 4 times slower than normal. 
- Using `__slots__`
  - Too many small objects can cause problems.
  - Object attributes are stored in `__dict__` which is 1/3 empty
  - `__slots__` removes `__dict__` (Con: attributes can't be added)
  - Use memory profiler to check memory when using `__slots__`. (Memory reduced to almost half, hence also
      makes faster since they can fit into CPU cache line, which is faster to
      access than main memory)
- using built-ins

  Eg. Sorting tasks according to priority

  ```python
  sorted(tasks, key = lambda task: task[1])
  ```

  Lambda function is called once per object, hence total complexity is not
  `n logn` due to caching.

  But there are functions written in C but faster.

  ```python
  from operator import itemgetter
  sorted(tasks, key = itemgetter(1))
  ```

  Similar built in functions which are written in C and are faster

  - `attrgetter()` - gets attribute to return
  - `sum()`
  - `max()`

- Allocate
  
  ```python
  """Fixed list allocation"""

  def allocz(size):
      """Alloc zeros with range"""
      return [0 for _ in range(size)]


  def allocz_fixed(size):
      """Alloc zeros with *"""
      return [0] * size

  ```  
  The second is ten times faster. When list is created and appended, python
  needs to reallocatr memory for the list. To avoid reallocation on every
  append, the list grows in fixed sizes. The sizes are 0, 4, 8, 16, 25, etc.

  However, in the second approach, we know the size of the list in advanced and
  hence is created in one allocation.

  While using this, make sure you initialize with immutable elements, since it
  is duplicated otherwise. Another option is use numpy's `np.zeros(size)`

- Make approximations if possible. It is okay to cheat. E.g. 1.1 * 1.1 doesn't
return accurate result.
