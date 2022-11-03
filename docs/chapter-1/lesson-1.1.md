<img src="../assets/images/logo.png" width=30% />

<hr>
<span style="display:flex; justify-content: space-between;">
    <a href="../index.html">Home</a> <a href="../chapter-1/lesson-1.2.html">Lesson-1.2</a>    
</span> 
<hr>

# Lesson-1.1

[TOC]

## Python shell | Replit Console

In this lesson, we will be working with the Python interpreter in Interactive Mode. TIt is also often called the Python shell. It is a tool that lets us execute individual lines of code and see the output right away. We will drop the phrase "interactive mode" and just refer to it as the interpreter. Have a look at the official Python documentation for more details about the [Python Interpreter](https://docs.python.org/3/tutorial/interpreter.html). If you have Python installed on your system, then the Python shell will look like this:

<img title="" src="../assets/images/img-001.png" alt="image-20210310105155189" style="zoom:80%;" data-align="center">

In Replit, this corresponds to the console screen on the right of the repl. This will be our playground for quite sometime:

<video controls loop autoplay muted>
    <source src="../assets/videos/prompt.mp4" type="video/mp4" zoom=50%>
</video>

## Prompts

<img title="" src="../assets/images/img-003.png" alt="" style="zoom:100%;" data-align="center">

The orange symbol that is displayed above is called a prompt. Its role is similar to that of the blinking cursor while editing documents. It is an invitation to type code. Code that is typed at the prompt is executed by the interpreter. In these lessons, we will use the following symbol to refer to the prompt: `>>>`.

We are all set to write our first line of code:

```python
>>> print('Hello World!')
Hello World!
```

Fire up a repl and type the code in the console. You should be getting the output on the next line.

## Output

Let us take a closer look at the first line of code that we wrote. `print` is called a built-in function in Python. A function is an object that accepts inputs and returns outputs. The term built-in refers to the fact that this function is something that is readily provided by Python for our use.

```python
>>> print('Hello World!')
Hello World!
>>> print("Hello World!")
Hello World!
```

The sentence enclosed by the parentheses of the `print` function is called a **string**. A **string** is a sequence of characters enclosed in quotes. Strings can either be in single quotes or double quotes. However, a single quote can't be matched against a double quote to enclose a string. We have used single quotes in line 1 and double quotes in line 3. Both lines give identical outputs. The ability to use both single quotes and double quotes comes in handy in situations like this:

> Print a string that has an apostrophe in it:

```python
>>> print("India's capital is New Delhi.")
```

Run the code given above and observe the output. `print` can also be used to print numbers:

```python
>>> print(1)
1
>>> print(2.0)
2.0
```

Multiple items can be printed on the same line in the following way:

```python
>>> print(1, 2)
1 2
>>> print('online', 'degree', 'program')
online degree program
```

Notice the presence of a space between successive elements? `print` automatically seperates multiple values with a delimiter, which is space by default.

If the `print` command is called without passing any input to it, then it prints a blank line:

```python
>>> print()

>>>
```

What happens if we just use type `print` without having the parentheses?

```python
>>> print
<built-in function print>
```

We don't get an error. Instead, the message is that `print` is a built-in function. But when you try the following code:

```python
>>> print 'Hello World!'
  File "<stdin>", line 1
    print 'Hello World!'
          ^
SyntaxError: Missing parentheses in call to 'print'. Did you mean print('Hello World!')?
```

The interpreter hits back with a `SyntaxError`. Like human languages, programming languages have their own syntaxes that have to be followed to convey your commands to the computer. Programming language syntaxes, however, are far more strict and have to be followed exactly in order to run your code. Parantheses are used to execute and pass values (called arguments in programming jargon) to functions like `print` . Note the lack of parentheses in the above snippet which is also pointed out by the handy error message. We will learn the syntax for various concepts in python in the upcoming lessons.

## Emojis

Before we jump into the serious stuff, let us try and print some emojis!

<img src="../assets/images/img-023.png" style="zoom:80%;" />

Try this out in your repl! A full list of emojis can be found [here](https://unicode.org/emoji/charts/full-emoji-list.html).

## Literals and Variables

Strings like `'Hello World!'` and numbers like `1`, `2.0` are called literals in Python. Formally, a literal is something that describes a constant value. Variables are containers that are used to store values. Variables in Python are defined in the following way:

```python
>>> x = 1
>>> print(x)
1
>>> y = 'a string'
>>> print(y)
a string
>>> foo_bar = 123.456
>>> print(foo_bar)
123.456
```

`=` is called the assignment operator. Whenever the assignment operator is present in a statement, it is used for one of the following purposes:

- define a new variable
- update an existing variable

```python
>>> x = 1         # define a new variable
>>> x = x + 1     # update an existing variable
>>> print(x)
2
```

The assignment operator is evaluated from right to left. That is, the expression to the right of the assignment operator is evaluated first. This result is then assigned to the variable on the left. Variables will be taken up in greater detail in the lessons of the second chapter.

## Basic Data Types | type()

We will be looking at the following basic data types:

- Integer
- Float
- String
- Boolean

### Integer

The `int` type represents integers. Python provides a command called `type` to determine the type of an object:

```python
>>> print(1)
1
>>> type(1)
<class 'int'>
```

### Float

The `float` type represents real numbers:

```python
>>> print(1.0)
1.0
>>> type(1.0)
<class 'float'>
```

The following is also a valid float literal:

```python
>>> print(1.)
1.0
```

`1.` and `1.0` are one and the same literal.

### String

The `str` type represents strings:

```python
>>> print('one')
one
>>> type("one")
<class 'str'>
```

### Boolean

The `bool` type represents boolean values:

```python
>>> print(True)
True
>>> type(False)
<class 'bool'>
```

Please note that `bool` values are case sensitive. That is, `true` and `false` are not `bool` values.

## Comments

A comment is a line of text that is not executed by the interpreter. Comments begin with the `#` symbol. The following are comments:

```python
>>> # This is a comment
>>> # print(1)
>>> 
```

As line-2 is a comment, `1` is not printed in the next line. Comments can also come at the end of a line of code:

```python
>>> print(1) # This line is printing the value 1
1
```

Adding comments is one of the ways to make code more readable. Its use will become clear in subsequent chapters.
