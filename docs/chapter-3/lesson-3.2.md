# Lesson-3.2

## Loops

### `#!py for` loop

Let us look at a simple problem of printing numbers. We would like to print the first 5 non-negative integers. We could do this using a while loop but let's try a different kind of a loop now, the `#!py for` loop:

```python linenums="1"
for i in range(5):
    print(i)
# A dummy line
```

The output is:

``` linenums="1"
0
1
2
3
4
```

`#!py for` and `#!py in` are keywords in Python. `#!py range` is an object that represents a sequence of numbers. Line-2 is the body of the loop. An intuitive understanding of the code given above is as follows:

- In each iteration of the loop, an element *in* the sequence is picked up and is printed to the console.
- Assuming that the sequence is ordered from left to right, the leftmost element is the first to be picked up.
- The sequence is processed from left to right.
- Once the rightmost element has been printed to the console, control returns to line 1 for one last time. Since there are no more elements to be read in the sequence, the control exits the loop and moves to line 3.

A visual representation is given below:

![control flow of for loop](../assets/images/img-018.png)

Similar to `#!py while` loops and `#!py if`-`#!py else` blocks, the body of a `#!py for` loop should be indented.



### range()

Now let's dive a bit deeper into this `#!py range()` function that we have been using. This function predictably returns a sequence, or a range if you will, of numbers. `#!py range(5)` results in the following sequence: $0, 1, 2, 3, 4$. In general, `#!py range(n)` creates the sequence:  $0, 1, ..., n - 1$. `#!py range` is quite versatile. The following code prints all two digit numbers greater than zero:

```python linenums="1"
for i in range(10, 100):
    print(i)
```

`#!py range(10, 100)` represents the sequence $10, 11, ..., 99$. In general, `#!py range(start, stop)` represents the sequence `start, start + 1, ..., stop - 1`. Let us add another level of complexity. The following code prints all even two digit natural numbers:

```python linenums="1"
for i in range(10, 100, 2):
    print(i)
```

`range(10, 100, 2)` represents the sequence `10, 12, ..., 98`. In general, `range(start, stop, step)` represents the sequence `start, start + step, start + 2 * step, ..., last`, where `last` is the largest element in this sequence that is less than `stop`. This is true when the `step` parameter is positive.

The following are equivalent:

- `#!py range(n)`
- `#!py range(0, n)`
- `#!py range(0, n, 1)`

So far we have seen only increasing sequences. With the help of a negative step size, we can also come up with decreasing sequences. The following code prints all two-digit even numbers greater than zero in descending order:

```python linenums="1"
for i in range(98, 9, -2):
    print(i)
```

For a negative `step` value, `#!py range(start, stop, step)` represents the sequence `start, start + step, start + 2 * step, ..., last`, where `last` is the smallest element in the sequence greater than `stop`.

Now, consider the following code:

```python linenums="1"
for i in range(5, 5):
    print(i)
```

`#!py range(5, 5)` is an empty sequence. So, the above code will not print anything. Another instance of an empty sequence:

```python linenums="1"
for i in range(10, 5):
    print(i)
```

The point to note is that neither of these code snippets produces any error. Finally, try executing the following snippet and observe the output.

```python
##### Alarm! Wrong code snippet! #####
for i in range(0.0, 10.0):
    print(i)
##### Alarm! Wrong code snippet! #####
```



### Iterating through Strings

Since a string is a sequence of characters, we can use the `#!py for` loop to iterate through strings. The following code will print each character of the string `x` in one line:

```python linenums="1"
word = 'good'
for char in word:
    print(char)
```

The output is:

``` linenums="1"
g
o
o
d
```

We can add some more code to enrich the output:

```python linenums="1"
word = 'good'
count = 1
for char in word:
    print(char, 'occurs at position', count, 'in the string', word)
    count = count + 1
```

The output is:

``` linenums="1"
g occurs at position 1 in the string good
o occurs at position 2 in the string good
o occurs at position 3 in the string good
d occurs at position 4 in the string good
```



