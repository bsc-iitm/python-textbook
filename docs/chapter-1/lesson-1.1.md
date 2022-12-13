# Lesson-1.1

## Python shell | Replit Console

In this lesson, we will be working with the Python interpreter in Interactive Mode. It is also often called the Python shell. It is a tool that lets us execute individual lines of code and see the output right away. We will drop the phrase "interactive mode" and just refer to it as the interpreter. Have a look at the official Python documentation for more details about the [Python Interpreter](https://docs.python.org/3/tutorial/interpreter.html). If you have Python installed on your system, then the Python shell will look like this:

<div class="center" markdown>
  ![Python IDLE](../assets/images/img-001.png)
</div>

In Replit, this corresponds to the console screen on the right of the repl. This will be our playground for quite sometime:

![type:video](../assets/videos/prompt.mp4)

## Prompts

![Replit prompt](../assets/images/img-003.png)

The orange symbol that is displayed above is called a prompt. Its role is similar to that of the blinking cursor while editing documents. It is an invitation to type code. Code that is typed at the prompt is executed by the interpreter. In these lessons, we will use the following symbol to refer to the prompt: `#!pycon >>>`.

We are all set to write our first line of code:

```pycon linenums="1"
>>> print('Hello World!')
Hello World!
```

Fire up a repl and type the code in the console. You will be getting the output on the next line.

## Output

Let us take a closer look at the first line of code that we wrote. `#!py print()` is something that is called a built-in function in Python. A function is an object that accepts inputs and returns outputs. The term built-in refers to the fact that this function is something that is readily provided by Python for our use. Follow along with and execute the codes given here as you go.

```pycon linenums="1"
>>> print('Hello World!')
Hello World!
>>> print("Hello World!")
Hello World!
```

The sentence enclosed by the parentheses of the `#!py print()` function is called a **string**. A **string** is a sequence of characters enclosed in quotes. Strings can either be in single quotes or double quotes. However, a single quote can't be matched against a double quote to enclose a string. We have used single quotes in line 1 and double quotes in line 3. Both lines give identical outputs. Now with the knowledge you have, attempt the solve the problem below.

!!! question " " 
    Print a string that has an apostrophe in it. The ability to use both single quotes and double quotes comes in handy in situations like this.
    ??? success "Solution"
        ```pycon
        >>> print("India's capital is New Delhi.")
        ```


Multiple items can be printed on the same line in the following way:

```pycon linenums="1"
>>> print(1, 2)
1 2
>>> print('online', 'degree', 'program')
online degree program
```

Notice the presence of a space between successive elements? `#!py print()` automatically seperates multiple values with a delimiter, which is space by default.

If the `#!py print()` function is called without passing any input to it, then it prints a blank line:

```pycon
>>> print()

>>>
```

What happens if we just use type `#!py print` without having the parentheses?

```pycon
>>> print
<built-in function print>
```

We don't get an error. Instead, the message is that `#!py print` is a built-in function. But when you try the following code:

```pycon
>>> print 'Hello World!'
  File "<stdin>", line 1
    print 'Hello World!'
          ^
SyntaxError: Missing parentheses in call to 'print'. Did you mean print('Hello World!')?
```

The interpreter hits back with a `#!pycon SyntaxError`. Like human languages, programming languages have their own syntaxes that have to be followed to convey your commands to the computer. Programming language syntaxes, however, are far more strict and have to be followed exactly in order to run your code. Parentheses are used to execute and pass values (called arguments in programming jargon) to functions like `#!py print()` . Note the lack of parentheses in the above snippet which is also pointed out by the handy error message. We will learn the syntax for various concepts in python in the upcoming lessons.

`#!py print()` can also be used to print numbers:

```pycon linenums="1"
>>> print(1)
1
>>> print(2.0)
2.0
```
Notice the lack of quotation marks. Try running  the 

## Emojis

Before we jump into the serious stuff, let us try and print some emojis!

```pycon
>>> print('\N{smiling face with smiling eyes}')
😊
>>> print('\N{grinning face}')
😀
>>> print('\N{smiling face with halo}')
😇
>>> print('\N{thinking face}')
🤔
```

Try this out in an interpreter of your choice! A full list of emojis can be found [here](https://unicode.org/emoji/charts/full-emoji-list.html).

## Literals and Variables

Strings like `'Hello World!'` and numbers like `1`, `2.0` are called literals in Python. Formally, a literal is something that describes a constant value. Variables are containers that are used to store values. Variables in Python are defined in the following way:

```pycon
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

```pycon
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

```pycon
>>> print(1)
1
>>> type(1)
<class 'int'>
```

### Float

The `float` type represents real numbers:

```pycon
>>> print(1.0)
1.0
>>> type(1.0)
<class 'float'>
```

The following is also a valid float literal:

```pycon
>>> print(1.)
1.0
```

`1.` and `1.0` are one and the same literal.

### String

The `str` type represents strings:

```pycon
>>> print('one')
one
>>> type("one")
<class 'str'>
```

### Boolean

The `bool` type represents boolean values:

```pycon
>>> print(True)
True
>>> type(False)
<class 'bool'>
```

Please note that `bool` values are case sensitive. That is, `true` and `false` are not `bool` values.

## Comments

A comment is a line of text that is not executed by the interpreter. Comments begin with the `#` symbol. The following are comments:

```pycon
>>> # This is a comment
>>> # print(1)
>>> 
```

As line-2 is a comment, `1` is not printed in the next line. Comments can also come at the end of a line of code:

```pycon
>>> print(1) # This line is printing the value 1
1
```

Adding comments is one of the ways to make code more readable. Its use will become clear in subsequent chapters.
