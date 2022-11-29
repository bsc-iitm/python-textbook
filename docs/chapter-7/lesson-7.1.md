# Lesson 7.1

## File Handling

### Why files

<!-- Add a section on what files are, then explain how they are stored in memory -->

The best way to motivate files is to take the human example. Consider our memory. There is a certain volume of information that we can retain in our working memory. A popular claim is that we can retain around seven chunks of information in our short-term memory. Anything that exceeds this volume of information, we have to resort to external aids such as notebooks.

Something similar happens in computers. Modern day computers are quite powerful and can retain several chunks of information at a time. Though computers are machines, the amount of short-term memory that they possess is still finite. This is where the idea of external storage comes in. Files are to computers what books are to humans. A file is used to record information in a permanent location so that it can be retrieved as and when needed.



### File handling

We are all used to opening files in our computers by simply double clicking on an icon. Let us take the example of a simple file having the following contents:

```
Income		Expenditure
12,000		10,000
50,000		45,000
75,000		35,000
14,000		12,000
60,000		40,000
```

This file has the income-expenditure details of a family for five months. We wish to create a new file that has the savings details added as a third column. That is, we wish to generate the following file:

```
Income		Expenditure		Savings
12,000		10,000			2,000
50,000		45,000			5,000
75,000		35,000			40,000
14,000		12,000			2,000
60,000		40,000			20,000
```

This seems like a simple task. Open this file, plug the numbers in the calculator, get the result and paste it in a new column and we are done. But what if the number of entries in the file increases? For example, let us say we wish to perform this operation for all families in the neighborhood. If we have 10 years worth data for 1000 families, we are looking at $1000 * 10 * 12 = 120,000$ entries! Our calculator will break down and so will we out of exhaustion.

This is where Python comes to our rescue. We can write a piece of code to automate the whole process. And all it is going to take is a few lines of code! In the next few lessons, we will see how to process files. We will learn the following operations:

- opening a file and closing it
- reading from a file
- writing to a file

File handling is an umbrella term that denotes all these operations.