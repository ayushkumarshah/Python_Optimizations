# Other Tips

- Use numpy if numerical several computations required.
- Use numba

  language level optimization is difficult as Python is dynamically interpreted language.
  Using JIT(Just In Time) Compilation - for functions which runs multiple times.

  E.g. calculating polynomial functional value from coefficients.

  ```python
  import numba

  @numba.jit
  def fun(args):
      ....
      ## no change
  ```

  Can also run in GPU and works better if type information provided in
  decorator.

- Use cython
  - Superset of Python  - Python + type connections to C libraries
  - C compiler required 
  - Written as .pyx files
  - See example code
  - Disadvantages:
    - Build step required
    - Model dependent on architecture (OSx will not work in Windows)

- Using other implementations of Python
    - Jython (written in JAVA)
    - MicroPython (optimized for MicroController)
    - IronPython (written in .NET)
    - PyPy (written in Python, includes a JIT compiler)


- Use C Extensions - Python C API
- Design and Code Reviews - Prepare a checklist
- Use Pytest Benchmarks
- Monitoring and Alerting
