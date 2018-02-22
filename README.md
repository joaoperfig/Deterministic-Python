# Deterministic-Python
### A programming language based on Python that fixes complexity problems with some recursive functions.

Deterministic Python is your usual Python3 in every way except that you can define some functions as:
```python
deterministic function(arguments):
    do(stuff)
	...
	return result
```
Functions can be defined as deterministic if the return product is always the same for the same arguments.
A cache of return values is kept for each deterministic function to optimize runtime.

## How to use the interpreter:
1. Place "deterministic" file next to your .dpy code
2. Run your code with "python deterministic yourcode.dpy"

## Comparison with regular python

Here's the poster child of exponential time complexity in Python:
```python
def fib(n):
    if (n<=1):
        return 1
    return fib(n-1) + fib(n-2)
```
And here is the its equivalent in Deterministic Python
```python
deterministic fib(n):
    if (n<=1):
        return 1
    return fib(n-1) + fib(n-2)
```
And here is a nifty graph comparing runtimes(seconds) for the first 35 numbers of the Fibbonacci sequence:

![alt text](https://image.ibb.co/foSnOH/comparision.png "time graph")

The red line that is always on zero is Deterministic Python

## Warnings

1. You cannot use the word "deterministic" outside the mentioned context.
2. Code must be indented with spaces only.
3. Deterministic Python still has the default recursion depth, so while fib(2000) can be calculated almos instantly here it would still raise a maximum recursion exception.
