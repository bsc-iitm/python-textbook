# Lesson-4.4

## Function calling Function

Consider the following program:

```python linenums="1"
def first():
    second()
    print('first')

def second():
    third()
    print('second')

def third():
    print('third')
    
first()
```

When the code given above is executed, the output is as follows:

```python
third
second
first
```

We have already seen that a function can be called from inside another function. The code snippet given above is a slightly complex example demonstrating this idea. Let us try to understand this visually. The method of visualization we'll employ here is novel and is called the **traffic-signal** method. You'll soon understand the motive behind naming it this way.

Consider a simple function which doesn't call any other function within its body. Most of the functions we have seen so far are of this type. The call corresponding to this function could be in one of these two states: ongoing or completed.

- **Ongoing** if the control is inside the body of the function, executing one of its lines. 
- **Completed** if all the lines in the body of the function have been executed and control has exited out of the function, either because a `#!py return` statement was encountered or because the control reached the last line in the function, in which case `#!py None` is returned by default.

While, a function which calls another function inside it could find itself in one of three states: ongoing, suspended or completed. Let's use the below color code to represent these three states:

![](../assets/images/img-033.png)

Now you see why it's called the traffic-signal method. Here, ongoing and completed have the same meanings as we've defined above. To understand the suspended state, consider the following diagrams that correspond to the code given above:

![](../assets/images/img-037.png)

Each column here represents what we call a _stack_ in programming jargon. They all represent the same stack at different instants of time, i.e., the  columns here show the state of the stack at three different time instants. The horizontal arrow shows the passage of time. The vertical arrow indicates that each new function call gets added onto the top of the stack — and whenever a new function is called, the previous function in the stack enters the suspended state.

![](../assets/images/img-038.png)

Re-introducing the code for reference:

```python linenums="1"
def first():
    second()
    print('first')

def second():
    third()
    print('second')

def third():
    print('third')
    
first()
```

As `third()` doesn't call any other function, it never enters the suspended state. The print statement in line-10 is the first to be executed; this is why we see `third` as the first entry in the output. The job of the function `third` is done and it turns red indicating it's completion. Now, the control transfers to the most recently suspended function - `second`. The execution of `second` resumes from the point where it got suspended; the print statement at line-7 is executed following which `second` turns red. Finally, control transfers to `first`, the print statement at line-3 gets executed and `first` also turns red.



## Recursion

A recursive function is one which calls itself inside the body of the function. A typical example of recursion is the factorial function:

```python linenums="1"
def fact(n):
    if n == 0:
        return 1
   	return n * fact(n - 1)
```

In the `fact` function given above, when the interpreter comes to line-4, it sees a recursive call to `fact`. In such a case, it suspends or temporarily halts the execution of `fact(n)` and starts executing `fact(n - 1)`. Let's take a look into a concrete example. This is what happens when `fact(4)` is called:

![](../assets/images/img-034.png)

When `fact(0)` is called, there are no more recursive calls. This is because, the condition in line-2 evaluates to `True` and the value `1` is returned. Such a condition is called the _base-case_ of a recursive function. In the absence of a base-case, the recursion continues indefinitely and never terminates.



![](../assets/images/img-035.png)

Once the base-case kicks in, `fact(0)` is done with its duty. So, the control transfers to the most recent suspended function. On the stack, we see that this is `fact(1)`. `fact(1)` now becomes active. When it returns the value `1`, its life comes to an end, so the control transfers to the most recent suspended function, which is `fact(2)`. This goes on until we reach `fact(4)`. When control exits `fact(4)`, the function finally returns the value `24`; all calls have been completed and we are done!



## Caution in Recursion

This section discusses some finer aspects of recursion.

### Fibonacci series

Let us take another popular example, the Fibonacci series:
$$
1, 1, 2, 3, 5, 8, ...
$$
Each term in this series is obtained by summing the two terms immediately to its left. We can mathematically express this as follows. If $x_1 = x_2 = 1$, then for all $n > 2, n \in \mathbb{N}$, we have the following recurrence relation:
$$
x_n = x_{n - 1} + x_{n - 2}
$$
We can now compute the $n^{th}$ term of the Fibonacci series using a recursive function:

```python linenums="1"
def fibo(n):
    if n == 1 or n == 2:
        return 1
    return fibo(n - 1) + fibo(n - 2)
```

Now, try calling `fibo(40)`. You will notice that it takes a very long time to compute the value. Why does this happen? This is because a lot of wasteful computation happens. Let us see why:

![](../assets/images/img-036.png)

This is a different representation of the recursive computation and is called a recursion tree. Notice how some function calls appear multiple times. `fibo(3)`  and `fibo(1)` are being computed twice, `fibo(2)` is being computed thrice. For a larger value of `n` such as `50`, there would be even more wasteful computation.

How can we estimate the time that it takes for this program to run? One way would be to sit in front of the computer with a stopwatch in hand. But that is so _un-Pythonic_. Thankfully, the `time` library provides a more practical solution to this problem:

```python linenums="1"
import time

def fibo(n):
    if n == 1 or n == 2:
        return 1
    return fibo(n - 1) + fibo(n - 2)

start = time.time()
fibo(40)
end = time.time()
print(f'It took approximately {round(end - start)} seconds.')
```

The output on a standard Python repl as recorded on the day of writing this lesson is:

```
It took approximately 118 seconds.
```

It takes almost two minutes! That's definitely a lot of wasted time. So for the problem of Fibonacci series, we see that naive recursion doesn't give us an efficient solution. A better approach here would instead be an iterative solution as follows:

```python linenums="1"
import time

def fibo(n):
    if n == 1 or n == 2:
        return 1
    x_prev, x_curr = 1, 1
    while n > 2:
        x_prev, x_curr = x_curr, x_prev + x_curr
        n -= 1
    return x_curr

start = time.time()
fibo(40)
end = time.time()
print(f'It took approximately {round(end - start)} seconds.')
```

Line-8 in the above code might be a bit confusing. This is nothing but a multiple assignment of two variables in the same line done simultaneously. The RHS of the assignment statement will be evaluated first, these two values will then be simultaneously assigned to their respective variable names on the LHS. A better and more accurate explanation for multiple assignment will be given in the next chapter when we discuss tuples.



### Counting Function Calls

How do we compute the number of times a function is called? We can do this using a global variable:

```python linenums="1"
def fact(n):
    global count
    count = count + 1
    if n == 0:
        return 1
    return n * fact(n - 1)

count = 0
fact(4)
print(count)
```

This is one of the potential uses of the `#!py global` keyword.



### Turtles all the way down

What happens if we have a recursive function without a base case? The simplest example of such a pathological function is:

```python linenums="1"
##### Alarm! Bad code snippet! #####
def foo():
    foo()

foo()
##### Alarm! Bad code snippet! #####
```
When this code is run we get an error message saying:

```pycon
Traceback (most recent call last):
  File "/home/main.py", line 4, in <module>
    foo()
  File "/home/main.py", line 2, in foo
    foo()
  File "/home/main.py", line 2, in foo
    foo()
  File "/home/main.py", line 2, in foo
    foo()
  [Previous line repeated 996 more times]
RecursionError: maximum recursion depth exceeded
```

This is a safeguard built into programming languages to prevent a stack overflow[^1] error - where a program tries to use more memory for a call stack than it was supposed to. The number of nested recursive calls in a stack is called the recursion depth of the stack and the limit for this depth is usually set to 1000 in most systems. If a program tries to exceed this limit, it triggers the fail safe mechanism as seen above and the program gets terminated. If you'd like to verify what the maximum recursion depth is for your system, you can run the following code:

[^1]: Did you know that the name [Stack Overflow](https://stackoverflow.com/) was selected from among a list of other names after a [a poll](https://blog.codinghorror.com/help-name-our-website/) held by one of the founders of the website?

```python
import sys
print(sys.getrecursionlimit())
```

