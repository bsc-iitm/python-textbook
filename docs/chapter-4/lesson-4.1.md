# Lesson-4.1

## Functions

### Introduction

In mathematics, a function is any object that accepts one or more inputs and produces one or more outputs. For example, $f(x) = x^2$, is a function that accepts a number and returns the square of that number. Functions in Python play a similar role, but are much more richer than their mathematical counterparts. Let us quickly convert the mathematical function, $f(x) = x^2$,  into a Python function:

```python linenums="1"
def f(x):
    y = x ** 2
    return y
```

The code given above is called the **definition** of the function `f`. Lines 2 and 3 make up the body of the function and are indented. The body of a function is a collection of statements that describe what the function does. Here,

- `#!py def` - is the keyword used to define functions
- `f` - is the name we have given to the function
- `x` - is a parameter (or input) we give to the function
- `#!py return` - is a keyword used to return (or output) the value `y` from the function

If we run the above code, we will not get any output. Functions are not executed unless they are called. The following code demonstrates what a **function call** looks like:

```python linenums="1"
def square(x):
    y = x ** 2
    return y

print(square(2))
```

The output is:

```
4
```

`#!py square(2)` is a function call. We use the name of the function, `square` and pass the number 2 as an argument to it. Keep in mind that though the words parameter and argument are often used interchangeably, technically they are two different terms. A _parameter_ is a variable in a function definition. It could be thought of as a placeholder. An _argument_ on the other hand is the value passed to a function when it is called. So in the above code we have, the `x` in line 1 is a parameter and the `#!py 2` in line 5 is an argument.

A visual representation of the terms we have defined so far is given below:

![functions](../assets/images/img-010.png)

A mental model to better understand functions:

- Parameters as we've seen so far are the inputs to the function.
- The body of the function can be pictured as the sequence of steps that transform the input to the output.
- The return statement can be thought of as a means of communicating the output to the rest of the code.

### Examples

Now let's look at some more examples of function definitions keeping the focus on the various syntactical aspects of functions in python.

- We can have functions with multiple parameters:

```python linenums="1"
# This function computes the area of a rectangle.
# Length and breadth are the parameters
def area(l, b):
    return l * b
```

- We can also have functions with no parameters at all:

```python linenums="1"
def foo():
    return "I don't like arguments visiting me!"
```

- Functions could also be defined with no return value:

```python linenums="1"
def foo():
    print("I don't like talking to the outside world!")
    
foo()
```

When the code given above is executed, we get the following output:

```
I don't like talking to the outside world!
```

Note that we didn't have to type `#!py print(foo())`. We just had to call the function — `foo()` — since it already has the print statement inside it's body. But what happens if we type `#!py print(foo())`? We get the following output:

```
I don't like talking to the outside world!
None
```

If no explicit return statement is present in a function, `None` is the default value returned by it. When the interpreter comes across the `#!py print(foo())` statement, first the function `foo()` is evaluated. This results in the first line of the output. And since `foo()` has no explicit return statement, it returns `None` by default which gets printed to the second line of the output.

- A minimal Python function looks like the one given below:

```python linenums="1"
def foo():
    pass # pass can be used as a placeholder
```

`#!py pass` is a keyword in Python. When the interpreter comes across a `#!py pass` statement, it doesn't perform any computation and _passes_ control to the next line. The reason this is minimal is because it has only those features that are absolutely essential for a function definition to be syntactically valid: a function name and at least one statement in the body. 

Such functions might seem useless at first sight, but they do have their place in programming. While writing a complex piece of code, a coder may realize that they need to define a function to perform a specific task. But they might not know the exact details of the implementation or it may not be an urgent requirement. In such scenarios, they can make use of a minimal function like the one given above, using `#!py pass` as a placeholder that can be replaced with the actual function body as and when the need arises.

- Functions could have multiple return statements, but the moment the first return is encountered, control exits from the function:

```python linenums="1"
def foo():
    return 1
	return 2
```

`foo()` will always return 1. Line 3 is redundant. Thanks to `#!py if-else` statements we can always control which return gets executed, when there are multiple return statements:

```python linenums="1"
def evenOrOdd(n):
    if n % 2 == 0:
        return 'even'
	else:
        return 'odd'

print(evenOrOdd(10))
print(evenOrOdd(11))
```

The output is:

```
even
odd
```

Here, when `evenOrOdd` is called with an even number as argument, the return statement in line 3 is executed. When the same function is called with an odd number as argument, the return statement in line 5 is executed.

- Functions could also have multiple return values:

```python linenums="1"
# Accept only positive floating point numbers
def bound(x):
    lower = int(x)
    upper = lower + 1
    return lower, upper

y = 7.3
l, u = bound(y)
print(f'{l} < {y} < {u}')
```

The output is:

```
7 < 7.3 < 8
```

The exact mechanism of what happens here will become clear when we come to the lesson on tuples. In line 8, the first value returned by `bound` is stored in `l` and the second value returned by `bound` is stored in `u`.

- Functions have to be defined before they can be called. A function call cannot precede the function definition. For example:

```python linenums="1"
##### Alarm! Wrong code snippet! #####
print(f(5))

def f(x):
    return x ** 2
##### Alarm! Wrong code snippet! #####
```

When the above code is executed, it throws a `NameError`. Why does this happen? The Python interpreter executes the code from top to bottom. At line 2, `f` is a name that the interpreter has never seen before and therefore it throws a `NameError`. Recall that `NameError` occurs when we try to reference a name that the interpreter has not encountered before.

- Function calls can be used as part of expressions:

```python linenums="1"
def square(a):
    return a ** 2

x, y, z = int(input()), int(input()), int(input())
if square(x) + square(y) == square(z):
    print(f'{x}, {y} and {z} form the sides of a right triangle with {z} as the hypotenuse')
```

- Function calls cannot be assigned values:

```python linenums="1"
##### Alarm! Wrong code snippet! #####
def foo():
    return True

foo() = 1
##### Alarm! Wrong code snippet! #####
```

The above code throws a `SyntaxError`.

- Functions can be called from within other functions:

```python linenums="1"
def foo():
    print('I am inside foo')
    
def bar():
    print('I am inside bar')
    print('I am going to call foo')
    foo()
    
print('I am outside both foo and bar')
bar()
print('I am outside both foo and bar')
```

- Functions can also be defined inside other functions:

```python linenums="1"
def foo():
    def bar():
        print('bar is inside foo')
    bar()

foo()
```

Try calling `bar()` outside `foo()`. What do you observe?


<!-- Should move this section to later lessons -->

### Docstrings

Consider the following function:

```python linenums="1"
def square(x):
    """Returns the square of x."""
    return x ** 2
```

The string immediately below the function definition is called a docstring. From the Python [docs](https://www.python.org/dev/peps/pep-0257/#what-is-a-docstring):

> _A docstring is a string literal that occurs as the first statement in a module, function, class, or method definition. Such a docstring becomes the `__doc__` special attribute of that object._

Ignore unfamiliar terms such as "module" and "class". For now, it is sufficient to focus on functions. Adding the docstring to functions is a good practice. It may not be needed for simple and obvious functions like the one defined above. But as the complexity of the functions you write increases, docstrings can be a life saver for other programmers reading your code.

The docstring associated with a given function can be accessed using the `__doc__` attribute:

```python
print(square.__doc__)
```

This gives `Returns the square of x.` as output.



