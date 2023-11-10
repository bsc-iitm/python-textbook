# Lesson-4.3

## Scope

Consider the following code:

```python linenums="1"
def foo():
    x = 1
    print('This is a veritable fortress. None can enter here.')
    print('\N{smirking face}')
    
foo()
print(x)
```

This will give the following output:

```pycon
This is a veritable fortress. None can enter here.
😏
Traceback (most recent call last):
  File "main.py", line 7, in <module>
    print(x)
NameError: name 'x' is not defined
```

Why did the interpreter throw an an error in line-7? It tried to look for the name `x` and was unable to find it. But isn't `x` present in the function `foo`? Is the interpreter careless or are we missing something? The interpreter is never wrong! The region in the code where a name can be referenced is called its _scope_ - a _scope_ could be thought of as a box or a container that encloses a set of names or variables. Variables defined in one scope can only be used within that particular scope, and not in any other scope. If we try to reference a variable outside its scope, the interpreter will throw a `NameError`.



### Local vs Global

In the above example, the scope of the name `x` is **local** to the function; `x` has a meaningful existence only inside the function and any attempt to access it from outside the function is going to result in an error. Let's take a look at another example:

```python linenums="1"
y = 10
def foo():
    x = 1
    print('I can access both x and y')
    print(f'x = {x}, y = {y}')

foo()
```

Here, the name `y` is accessible from within the function as well. We say that the scope of `y` is **global**. That is, it can be referenced from anywhere within the program — even inside a function — after it has been defined for the first time. There is a slight catch though, if we have another variable with the same name inside the function definition, then things change. Let's keep that case aside for now.

At this stage, we are ready to formulate the rules for local and global scopes[^1]:

[^1]: [More on rules for local and global variables](https://docs.python.org/3/faq/programming.html#what-are-the-rules-for-local-and-global-variables-in-python)

- **Local Scope**: Whenever a variable is assigned a value anywhere within a function, its scope becomes local to that function. It can only be accessed from within the function body.

- **Global Scope**: Variables defined outside of any function are implicitly treated to be part of the global scope, making them accessible from any part of the program.

The scope of the parameters in a function definition are local. The following code will throw a `NameError` when executed:

```python linenums="1"
def double(x):
    x = x * 2
    return x

double(2)
print(x)
```



### Examples

Let's now look at a few more examples that bring out some of the finer points regarding local and global scope:

```python linenums="1"
### Variant-1
def foo():
    x = 1
    print('I can access both x and y')
    print(f'x = {x}, y = {y}')

y = 10
foo()
```

Notice the difference between this code and the one at the beginning of the earlier section. Here, the variable `y` is defined after the function definition, while in the earlier version `y` was defined before the function definition. But both versions would give the same output. Why? Because all that matters is for  `y` to be defined before the **function call**. What happens if `y` is defined after `foo` is called?

```python linenums="1"
### Variant-2
def foo():
    x = 1
    print('I can access both x and y')
    print(f'x = {x}, y = {y}')

foo()
y = 10
```

This throws a `NameError` at line-5, which is reasonable as `y` is not defined in the main program before `foo` is called. The scope of `y` is still global; it can be referenced anywhere in the program, but only after the point where it has been defined.

Now, let us crank up the difficulty level:

```python linenums="1"
def foo():
    x = 10
    print(f'x inside foo = {x}')

x = 100
foo()
print(f'x outside foo = {x}')
```

We have the same name `x` appearing both inside the function and outside the function. Are they the same or different? Let us check the output:

```
x inside foo = 10
x outside foo = 100
```

They are different! The `x` inside `foo` is different from the `x` outside `foo`. 

- The scope of the name `x` inside `foo` is local; it is a local variable. This is because of the first rule: a variable that is assigned a value inside the function becomes a local variable. Since `x` is assigned a value in line-2, it becomes a local variable.
- The scope of the `x` outside `foo` is global. Though there is another `x` inside the function `foo`, it cannot be accessed outside the function.

This may start to get a little confusing. How does Python internally manage local and global variables? For this, we will briefly turn to the concept of namespaces. This will give a different perspective to the problem of name resolution.



## Namespaces

Consider the following snippet of code:

```python linenums="1"
x = 1.0
avar = 'cool'
def foo():
    pass
```

We are using three different names here: `x`, `avar` and `foo`. The first two names represent variables that store literals. The last name represents a function. How does the Python interpreter internally process these names? It uses a system of _namespaces_. We can imagine a namespace as a mapping of every name we have defined to corresponding objects. It is used to store the values of variables and other objects in the program, and to associate them with a specific name.

![Namespace](../assets/images/img-021.png)

A typical python program uses different types of namespaces and these different namespaces are isolated from each other thus allowing us to use the same name for different variables or objects in different parts of our code, without causing any conflicts or confusion.

### `#!py globals()`

As we said there are different types of namespaces. The variables that we define in the main program body ie., outside any function body are stored in the `#!py globals` namespace. For example:

```python linenums="1"
x = 1.0
avar = 'cool'
def foo():
    y = 2.0

foo()
print(globals())
```

This returns the following output:

``` hl_lines="5"
{'__name__': '__main__', '__doc__': None, '__package__': None, '__loader__': 
<_frozen_importlib_external.SourceFileLoader object at 0x0000022009CA89A0>, 
'__spec__': None, '__annotations__': {}, '__builtins__': 
<module 'builtins' (built-in)>, '__file__': 'main.py',  '__cached__': None, 
'x': 1.0, 'avar': 'cool', 'foo': <function foo at 0x0000022009BE3E20>}
```

Ignore all the other details, for now just focus on the line highlighted in blue. Notice that the names `x`, `avar` and `foo` are present in the output which means that they are part of the `#!py global` namespace. `x`  and `avar` are mapped to the objects `#!py 1` and `#!py 'cool'` respectively, while `foo` is mapped to some complex looking object:  `<function foo at 0x0000022009BE3E20>`. The number `0x0000022009BE3E20` represents the location in the memory where the function's definition is stored [^2]. There is another way to check whether a given name is in the global namespace:

[^2]: Have a look at [this stackoverflow answer](https://stackoverflow.com/questions/19333598/in-python-what-does-function-at-mean) to know what `#!pycon <function 'somename' at 'somewhere'>` means

```python linenums="1"
print('x' in globals())
print('avar' in globals())
print('foo' in globals())
```

All three lines should result in `True`. 

### `#!py locals()`

Notice something interesting in the previous code, the name `y` does not seem to part of the `#!py globals` namespace! We can verify this as follows:

```python
print('y' in globals())
```

This results in `False`. Variables that are assigned a value inside a function are `local` to the function and cannot be accessed outside it. How does the Python interpreter handle names inside functions? - Simply by creating a new namespace separate from the global namespace every time a function is called. This new namespace is called a local namespace. Now, consider the following code:

```python linenums="1"
def foo():
    y = 2.0
	print('Is y in locals?', 'y' in locals())

foo()
print('Is y in globals?', 'y' in globals())
```

It returns the following output:

```
Is y in locals? True
Is y in globals? False
```



## Scope and Namespaces

Now that we have a good mental picture of what namespaces are, let's try to look at how the concept of scope ties in with namespaces. Consider the following example:

```python linenums="1"
def foo():
    print(y)
    print(locals())
    x = 1
    print(locals())

y = 10
foo()
```

This gives the output:

```
10
{}
{'x': 1}
```

Here, the interpreter creates a local namespace for `foo` when it is called in line-8. Since `y` is only being referenced inside `foo`, it doesn't become a part of the local namespace. It remains a global variable. `x` on the other hand is being assigned a value inside `foo`, therefore is enters the local namespace and is a local variable. The moment control exits the function `foo`, the namespace corresponding to it is deleted.

Whenever the interpreter comes across a name inside the body of a function, it sticks to the following protocol:

- First it peeps into the local namespace created for that function call to see if the name is present there. If it is present, then it goes ahead and uses the value that the name points to in the local namespace.
- If it is not present in the local namespace, then the interpreter moves to the global namespace. If it is present in the global namespace, the corresponding value found there is used for the name.
- If it is not found in the global namespace either, then it looks into the `built-in` namespace (We'll come back to the `built-in` namespace right at the end).
-  Finally if the interpreter could not find the name in any of these namespaces, then it raises a `NameError`. 

The following image captures this idea. We'll ignore the `built-in` namespace for now.


![](../assets/images/img-024.png)

 With this context, let us revisit the problem that we looked at the end of the first section:

```python linenums="1"
def foo():
    x = 10
    print(f'x inside foo = {x}')

x = 100
foo()
print(f'x outside foo = {x}')
```

We were getting the following output:

```
x inside foo = 10
x outside foo = 100
```

When the function is called at line-6, the interpreter creates a local namespace for `foo`. At line-2, `x` becomes a part of this namespace. When `x` is referenced at line-3, the interpreter first looks at the local namespace for `foo`. Since `x` is present there, it is going to use the value corresponding to it - in this case `10`.  Once control exits the function, the local namespace corresponding to `foo` is deleted. At line-7, the interpreter will replace the name `x` with the value `100` which is present in the global namespace.



## `#!py global` keyword

Let us revisit the scope rules:

- **Local Scope**: Whenever a variable is assigned a value anywhere within a function, its scope becomes local to that function. It can only be accessed from within the function body.

- **Global Scope**: Variables defined outside of any function are implicitly treated to be part of the global scope, making them accessible from any part of the program.

Now, consider the following code:

```python linenums="1"
def foo():
	print(x)
    x = x + 1

x = 10
foo()
```

When the above code is executed, we get the following error[^3]:

[^3]: [Example taken from python docs FAQ](https://docs.python.org/3/faq/programming.html#why-am-i-getting-an-unboundlocalerror-when-the-variable-has-a-value)

```pycon
Traceback (most recent call last):
  File "/home/main.py", line 6, in <module>
    foo()
  File "/home/main.py", line 2, in foo
    print(x)
UnboundLocalError: local variable 'x' referenced before assignment
```

Let's try to decode this error message: an `UnboundLocalError` is being traced back to line-2 that is part of the function `foo` - what does this mean? Basically the interpreter is trying to warn us that we are referencing a local variable at line-2 that doesn't have any value bound to it yet. The value of `x` in the global scope is not utilized because of our first rule for scopes, that is if we make an assignment to a variable inside a function, the variable becomes part of the local scope of the function thus shadowing any similarly named variable in the global scope. 

To reaffirm this point let's try running the above code without the assignment to `x` in the function body:

```python linenums="1"
def foo():
    print(x)

x = 10
foo()
```

This will work fine and output `10` as expected. But what if we intentionally want to reuse the global variable `x` and be able to assign it new values from within the function `foo`? Python provides a keyword called `global` for this purpose:

```python linenums="1"
def foo():
    global x
    print(f'x inside foo = {x}')
    x = x + 1
    print(f'x inside foo = {x}')
    
x = 10
print(f'x outside foo = {x}')
foo()
```

The output is:

```
x outside foo = 10
x inside foo = 10
x inside foo = 11
```

By declaring `x` to be global inside `foo`, we're telling the interpreter to use the value of `x`  available in the global namespace instead of associating it with a new value in the local namespace of `foo`.



## Built-ins

So far we have been blindly using built-in functions like `#!py print`, `#!py int`, `#!py input` and so on. At some level, these too are names in Python and these also get resolved during run-time. There is a separate namespace called `builtins` where all the built-in functions, data types and exceptions in python are defined and stored.

Consider the following code:

```python
##### Never do something like this! #####
print = 1
##### Never do something like this! #####
```

If the above code is executed, we don't get an error! Surprising right? This is because syntactically, there is nothing wrong here. But we will get into serious problems when we try to do the following:

```python
##### Alarm! Wrong code snippet! #####
print = 1
print(1)
##### Alarm! Wrong code snippet! #####
```

This will throw a `TypeError`. The name `#!py print` has been hijacked and is being used as a variable of type `#!py int`. How does Python allow this to happen?

![](../assets/images/img-025.png)

When resolving names, the built-in namespace is the last stage in the interpreter's journey. Syntactically, nothing prevents us from using the name of a built-in function, such as `#!py print`, as the name of a variable. But this is a very bad practice that should be avoided at any cost!

