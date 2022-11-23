# Lesson-6.2

## Text processing

The following paragraph is an excerpt from a talk given by Guido. The full text can be found [here](http://neopythonic.blogspot.com/2016/04/kings-day-speech.html). 

> In reality, programming languages are how programmers express and communicate *ideas* — and the audience for those ideas is other programmers, not computers. The reason: the computer can take care of itself, but programmers are always working with other programmers, and poorly communicated ideas can cause expensive flops. In fact, ideas expressed in a programming language also often reach the end users of the program — people who will never read or even know about the program, but who nevertheless are affected by it.

Text processing plays an important role in analyzing text data. Given a piece of text, the following are some of the basic questions that we can ask:

- How many sentences are there in the text?
- How many words are there in the text?
- How many of them are unique?
- Which word appears the most number of times?

Are these meaningful questions to ask? Do they lead us anywhere? Yes, they do! Consider the task of classifying articles. Some sample categories could be: lifestyle, science and technology, literature, films. If we want to understand what category an article falls under, one way to go about it is to read the entire article. We can do it for one or two articles, but what if we have to do this for hundreds of them? A better solution would be to computationally process each article, find the top five most common words and use that to get an idea of what the text is about.

We could program a solution to do exactly this. In the next few sections, we will gradually write, one step at a time, the code that answers all of the above questions. Follow along with an IDE or text editor of your choice and run the code at each step. Let's start off by storing the string in a variable `text`.

```python linenums="1"
text = "In reality, programming languages are how programmers express and communicate ideas — and the audience for those ideas is other programmers, not computers. The reason: the computer can take care of itself, but programmers are always working with other programmers, and poorly communicated ideas can cause expensive flops. In fact, ideas expressed in a programming language also often reach the end users of the program — people who will never read or even know about the program, but who nevertheless are affected by it."
```



### Number of sentences

Sentences could end with one of the following tokens: full stop, exclamation mark or question mark. For simplicity, let us assume that all sentences in our text ends with a full stop. We can split the string using full stop as a delimiter to get a list of sentences:

```python linenums="2"
sentences = text.split('.')
```
Let's now look into the list using some temporary code. It's very important as a programmer to know what your code is doing and printing out the contents of your variables will give a good look of what's happening.

```python
# Prints one sentence in each line
for sentence in sentences:
    print(sentence)
print(f'There are {len(sentences)} sentences in this text.')
```
##### Output
```linenums="1"
In reality, programming languages are how programmers express and communicate ideas — and the audience for those ideas is other programmers, not computers
The reason: the computer can take care of itself, but programmers are always working with other programmers, and poorly communicated ideas can cause expensive flops
In fact, ideas expressed in a programming language also often reach the end users of the program — people who will never read or even know about the program, but who nevertheless are affected by it

There are 4 sentences in this text.
```

Notice that there are only three sentences, but we get the output to be four in the last line. On closer inspection, we see that `#!py sentences[-1]` is not a sentence but an empty string. This is because, when a string is split using a delimiter which is present in the string, two substrings get generated, one to the left of the delimiter and the other to its right. As the full stop is the last character in the text, the substring to its right is an empty string. One way to correct this is to remove all empty strings in `sentences`:

```python linenums="3"
while '' in sentences:
    sentences.remove('')
print(f'There are {len(sentences)} sentences in this text.')    
```

##### Output
```
There are 3 sentences in this text.
```
One problem solved!



### Number of words

To get the number of words, we can split each sentence by space:

```python linenums="6"
words = [ ]
for sentence in sentences:
    words_ = sentence.split(' ')	# words_ contains words in sentence
    words.extend(words_)		    # words is the collection of all words
```

If we print out `#!py len(words)`, we get the number of words to be 86. Is that correct? [wordcounter.net](https://wordcounter.net/) claims that there are 82 words in this text. Clearly, something is wrong with our code. Let us print each word along with its index in separate lines and see what we have:

```python
for index, word in enumerate(words):
    print(index, word)
```

Sifting through the output, we notice the following offenders:

```
11 —
23 
49
67 —
```

Indices 11 and 67 are [em dashes](https://en.wikipedia.org/wiki/Dash) (—) while 23 and 49 correspond to empty strings. Since we have two different characters to remove, let us clean up the list in the following way:

```python linenums="10"
proc_words = [ ]
for word in words:
    if not(word == '' or word == '—'):
        proc_words.append(word)
print(f'There are {len(proc_words)} words in this text')
```

And we have 82 words as expected. One more problem solved!



### Number of Unique Words

You might be wondering why this lesson has come under Chapter 6 if there are no dictionaries floating around. This section will assuage that worry, because we will now use a dictionary to keep track of the number of unique words along with their frequency.

```python linenums="15"
uniq_words = dict()
for word in proc_words:
    if word not in uniq_words:
        uniq_words[word] = 0
    uniq_words[word] += 1
print(f'There are {len(uniq_words)} unique words in this text')
```

Apparently, there are 62 unique words in our text. Upon manual inspection, the word "programmers" occurs four times in the text. What does our dict have to say?

```python
print(uniq_words['programmers'])
```

We get `2` as the output, another wrong answer! Programming doesn't seem like magic after all. We are making mistakes far too often. Note that this is not the exception, but the norm. The nice part of making mistakes is that they are almost always an opportunity to learn something. An error in the code is hidden knowledge, an insight into a flaw in our logic that we are yet to unmask. Now, back to the drawing board. Let us search for all entries in the list `proc_words` that have the substring "programmers" in them:

```python
for word in proc_words:
    if 'programmers' in word:
        print(word)
```

##### Output

```
programmers
programmers,
programmers
programmers,
```

So, the problem is with the special character: comma.

Another problem is introduced by the capitalization of words, usually at the beginning of sentences. Now that the problems have been identified, let us go ahead and fix them. Of course, this means we have to go back and modify the code we have already written. This is a perfectly normal process in programming - You start writing your solution, you gain a new insight in the process, you go back and change what you had just written (or sometimes even throw away the whole thing and start from scratch!). Let's now generate `proc_words` the right way:

```python linenums="10"
proc_words = [ ]
for word_ in words:
    word = word_.lower()
    if not(word == '' or word == '—'):
        if not word_.isalnum():
            word = word_[:-1]
        proc_words.append(word)
print(f'There are {len(proc_words)} words in this text')
```

Several things are happening here. In line 12, every word is converted to lower case. In line , em dashes and empty strings are being ignored. Line 14 checks if a word contains a special character. If it does, then it is unburdened of that dangling character in line 15. Here we assume that special characters usually appear at the end of the word. In this text, there are two cases: "programmers," and "reason:". All processed words are finally added to `proc_words` in line 16. Now that we have a cleaned up `proc_words`, we can go back and generate `uniq_words`:

<!-- Idea for an exercise: remove special characters that don't occur at the end of the word -->

```python linenums="18"
uniq_words = dict()
for word in proc_words:
    if word not in uniq_words:
        uniq_words[word] = 0
    uniq_words[word] += 1
print(f'There are {len(uniq_words)} unique words in this text')
```

Lovely! There are 58 unique words in the text. We can check if this is right by printing all the words and their counts:

```python
for word, freq in uniq_words.items():
    print(word, freq)
```

We can see that there is no erroneous repetition of any word. As a test, we can also see if the sum of the counts gives back the total number of words:

```python
total = 0
for word in uniq_words:
    total += uniq_words[word]
assert total == len(proc_words)
```

As the code doesn't raise any `#!py AssertionError`, we are correct!



### Frequent Words

Now onto the last problem - let us find the top three most frequently occurring words:

```python linenums="24"
first_word = second_word = third_word = ''
first_val = second_val = third_val = 0
for word, freq in uniq_words.items():
    if freq > first_val:
        first_val, second_val, third_val = freq, first_val, second_val
        first_word, second_word, third_word = word, first_word, second_word
    elif freq > second_val and freq < first_val:
        second_val, third_val = freq, second_val
        second_word, third_word = word, second_word
    elif freq > third_val and freq < second_val:
        third_val = freq
        third_word = word
print(first_word, first_val)
print(second_word, second_val)
print(third_word, third_val)
```

##### output
```
the 6
programmers 4
in 3
```

We see that "programmers" is the second most frequent word. First and third most frequent words are "the" and "in" respectively. Such common words are called stop-words. If they are removed from the text,  "programmers" becomes the most frequent non-trivial word. So, without reading this text, one can guess that it should be something about programmers, thanks to Python!



### Summary

The main takeaway from this lesson is the kind of mistakes we made and the way we fixed each one of them. In almost every problem, we started off with a solution, then tested it. We figured out that something was wrong, so we went back and tried to fix the problem.
