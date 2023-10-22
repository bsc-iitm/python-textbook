# Lesson-0

## What is Python?
To answer this question, we need to first ask _What is a programming language?_ A **programming language** is essentially a language in which you can tell your computer what to do. You will understand what that means as start programming. Every programming language has its own strengths and purposes. **Python** is a general-purpose programming language that can be used for a wide variety of purposes including but not limited to data science, automation, machine learning and  software and web development. A typical python program to find the sum of the first 100 numbers looks like this:

```python linenums="1"
sum = 0
for number in range(1, 101):
  sum += number
print(sum)
```

Do not worry too much about how the code works right now, we'll get into that over the course of the book. But now let's address a question you might have right now - why do we need to complicate things with programming languages to tell the computer what to do when we have simple applications like calculators that can do the same? Let's do a boring experiment: Let's add all the numbers from $1$ through $100$ on a calculator. How long did it take you? Now let's run the following program: 

<iframe frameborder="0" width="100%" height="300px" src="https://replit.com/@BharathValaboju/sum-of-first-hundred-numbers?embed=true"></iframe>

How long did this code take you? Blazingly fast, isn't it? That's what coding enables you to do - Create ingenious solutions to problems. Programming also enables you to create applications. Applications like calculator that are designed for use by non-coders are created using code. Consider the following simple application. It takes two numbers as input and prints out their sum.

<iframe frameborder="0" width="100%" height="300px" src="https://replit.com/@BharathValaboju/simple-adder?embed=true"></iframe>

The codes for these programs are in `main.py` files which you can view by pressing the <span class="keys">
  <kbd>
    <svg preserveAspectRatio="xMidYMin" width="16" height="16" viewBox="0 0 24 24" fill="currentColor" aria-hidden="true" class="css-1gcl232" style="vertical-align: middle;">
      <path fill-rule="evenodd" clip-rule="evenodd" d="M2.25 4.5C2.25 3.25736 3.25736 2.25 4.5 2.25H19.5C20.7426 2.25 21.75 3.25736 21.75 4.5V7.5C21.75 8.07627 21.5334 8.60193 21.1771 9C21.5334 9.39807 21.75 9.92373 21.75 10.5V13.5C21.75 14.0763 21.5334 14.6019 21.1771 15C21.5334 15.3981 21.75 15.9237 21.75 16.5V19.5C21.75 20.7426 20.7426 21.75 19.5 21.75H8.5C7.25736 21.75 6.25 20.7426 6.25 19.5V16.5C6.25 15.9237 6.46664 15.3981 6.82292 15C6.46664 14.6019 6.25 14.0763 6.25 13.5V10.5C6.25 10.237 6.29512 9.98458 6.37803 9.75H4.5C3.25736 9.75 2.25 8.74264 2.25 7.5V4.5ZM19.5 8.25C19.9142 8.25 20.25 7.91421 20.25 7.5V4.5C20.25 4.08579 19.9142 3.75 19.5 3.75H4.5C4.08579 3.75 3.75 4.08579 3.75 4.5V7.5C3.75 7.91421 4.08579 8.25 4.5 8.25H19.5ZM8.5 9.75C8.08579 9.75 7.75 10.0858 7.75 10.5V13.5C7.75 13.9142 8.08579 14.25 8.5 14.25H19.5C19.9142 14.25 20.25 13.9142 20.25 13.5V10.5C20.25 10.0858 19.9142 9.75 19.5 9.75H8.5ZM19.5 15.75H8.5C8.08579 15.75 7.75 16.0858 7.75 16.5V19.5C7.75 19.9142 8.08579 20.25 8.5 20.25H19.5C19.9142 20.25 20.25 19.9142 20.25 19.5V16.5C20.25 16.0858 19.9142 15.75 19.5 15.75Z"></path>
    </svg> Show files
  </kbd>
</span> button. Come back and go through the code when you have learned some python.


## Why learn Python?

The strongest reason is utility. Python powers a large number of applications and is used by companies like Google, Netflix, Dropbox, Quora. A closely related reason is popularity. If a language is popular in the developer community, then there must be something good about it. In a 2022 [survey](https://survey.stackoverflow.co/2022/#most-loved-dreaded-and-wanted-language-want) conducted by the company StackOverflow, Python was rated as the second most wanted language.
 

![Stackoverflow survey](../assets/images/img-016.png)


Around 66% of the 65,000 developers who responded to the survey are currently developing with Python and have expressed interest in continuing to develop with it. Another strong reason to learn Python is that it lets us create beautiful things such as this animation[^1]:

![type:video](../assets/videos/sinx.mp4)

[^1]: Thanks to [Manim Community](https://docs.manim.community/en/v0.4.0/examples.html#special-camera-settings) for the source code. The code that was used to render this animation can be found [here](https://github.com/pypod/pypod.github.io/blob/main/code/lesson_0.py).

Being able to create something like this is the end goal of this course. Musicians create music; musical instruments are their tools. Painters create paintings; the brush and the canvas are their tools. Coders create software; programming languages are their tools. Python is one of the most versatile and accessible languages out there. Python was designed to be human readable and easy while also being very powerful. This quality makes python the perfect first programming language. We will start from the basics and systematically cover the important aspects of the language. 

!!! info "How easy is Python?"
    Python has a vast collection of libraries that makes it easy to implement complex tasks. This is well described by this cheeky comic[^2] that pops up when you enter `#!py import antigravity` in IDLE.


    <div style="display: flex; justify-content: center">
        ![Python Web comic](https://imgs.xkcd.com/comics/python.png)
    </div>

    [^2]: Credit to [xkcd.com](https://xkcd.com/353) for the comic



## Lessons

### Organization

This index is organized as a sequence of lessons. Lessons will be numbered as `<chapter>.<lesson>`. Each chapter will have about four lessons. These lessons are best read in the sequence in which they appear, starting from chapter-1 and going all the way up to chapter-12. If you are already familiar with Python, then have a look at the Table of Contents in the home page and jump into the lesson that seems least familiar.

Each chapter introduces one important programming concept in Python. This will be that chapter's title. This doesn't mean that all the lessons in the chapter will focus on only that particular concept. For example, chapter-2 introduces the idea of conditionals, but built-in functions and Python's standard libraries also feature in the same week.

The outline of the book is as follows:

- Chapter-1: Introduction to Python

- Chapter-2: Conditionals

- Chapter-3: Loops

- Chapter-4: Functions

- Chapter-5: Lists and Tuples

- Chapter-6: Sets and dictionaries

- Chapter-7: File handling

- Chapter-8: Object Oriented Programming

### How to read these lessons?

- Do not trust any piece of code blindly.
- Execute the code and observe the output.
- Think about the output. 
- Verify if the explanation given in text matches your observations.

Programming courses are among the few courses where the learner has an upper hand over instructors. No one can trick you. Code does not lie. All that is demanded of you is to make an effort to execute every snippet of code that you see in these lessons.

### Python Version

We will be using Python-3.8 or higher throughout these lessons. If some of you are already familiar with Python and are used to Python-2, it is strongly recommended that you shift to Python-3. This is not an arbitrary choice as Python-2 has reached the end of its life.

## Setting up Replit

Replit is an online environment where we can write code. It is an ideal place to learn programming and we will be using it extensively in this course. Head to [replit.com](http://www.replit.com/) and sign up using your Online Degree account. Replit provides an excellent [tutorial](https://docs.replit.com/getting-started/intro-replit) to get you started.

## Installing Python on your System

However, if you wish to use Python on your system, you can install it from [here](https://www.python.org/downloads/). You can refer to this [guide](https://www.javatpoint.com/how-to-install-python) to get a step-by-step process of installing Python. Having Python on your system will be useful in the subjects that you'll emcounter in the Diploma level.

## History

Python first appeared on the programming landscape 30 years ago, in February 1991. It was created as a hobby project by a Dutch programmer, Guido van Rossum. He served as the _[benevolent dictator for life](https://en.wikipedia.org/wiki/Benevolent_dictator_for_life)_ of Python’s development until 2018, when he stepped down from the post.

<figure markdown>
  ![Guido Van Rossum](../assets/images/guido.jpg)
  <figcaption markdown>Guido Van Rossum at the Dropbox Headquarters in 2014[^3]</figcaption>
</figure>

[^3]: Image-Source: [Wikipedia](https://en.wikipedia.org/wiki/Guido_van_Rossum#/media/File:Guido-portrait-2014-drc.jpg)

A popular question that gets asked often is how the language got its name. This is the answer from the official Python documentation:

> When he began implementing Python, Guido van Rossum was also reading the published scripts from [“Monty Python’s Flying Circus”](https://en.wikipedia.org/wiki/Monty_Python), a BBC comedy series from the 1970s. Van Rossum thought he needed a name that was short, unique, and slightly mysterious, so he decided to call the language Python.

Python is 30 years old. Programmers who boarded the Python-bus 30 years back lovingly talk of it as though it were a friend. This is not an exaggeration! This is a language that has been built by people like you and me, and is being used by thousands of people around the globe. Let us jump in with an open mind and see what it has to offer!

## Explore

1. Check out the website of the [Python Software Foundation](https://www.python.org/psf/) and get to know more about the organization behind Python.
2. Have a look at this interesting [interview](https://blog.dropbox.com/topics/work-culture/-the-mind-at-work--guido-van-rossum-on-how-python-makes-thinking) of Guido Van Rossum. This is a blog maintained by Dropbox. Another trivia: Guido worked at Dropbox for six and a half years. 
3. Try to watch documentaries and interviews on the web where Guido talks about how Python came into existence. It is always good to know about some non-technical aspects of the language, such as its history and something about the people who were behind its development. It gives a humanistic flavor to technology. We often forget that a lot of software is written by humans, for humans.
4. In the next few weeks to come, [StackOverflow](https://stackoverflow.com/) might become the most visited website by most of you. Some of you might be familiar with it, but for the others, StackOverflow is a question-answer forum for programming related questions. It is extremely popular not just among beginners but even experienced developers. Do check it out, but use it wisely. Refrain from using it to get answers to assignment questions; you won't learn anything that way.
5. You can also look into the official documentation on the python [website](https://docs.python.org/3/).
