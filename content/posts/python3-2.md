---
title: "Through Python3 (Day 2)"
date: 2019-02-16T00:18:00+05:30
draft: false
toc: true
author: Krishna Kumar Dey
tags: [ "python", "beginner"]
---



# Through Python3(Day 2)

Hola Everyone, the Previous day we learned about how everything in Python is an object and about Mutable and Immutable Datatypes. If You haven’t the go through the  [link]({{< ref "python3-1.md" >}})  and read about them and come back again to join us.

Today we will be talking about Conditionals and Loops.

## Conditionals
So first let me tell you all about Conditionals. Python provides two ways to treat conditionals. The first one is the native way.

![5](/images/python3-2/5.png)

Another one is the clearer, and the developers of Python tried to make it simpler and easy to understand.

![6](/images/python3-2/6.png)

Now let me tell you about some of the operators.

Python has a variety of operators like ( You can read about them from this  [link](https://theinvinciblecoder.wordpress.com/2018/05/13/through-python3about-operators/)

` + , – , += , == , != , AND , & . . . . . . . .  `


There is another type of operators called  __Special operators.__

` is `

` is not `

So how these special operators different from  ‘__==__’  and  ‘__!=__’

__is__  operator compares the id. Whereas  __==__  operator compares the value.

As I have told earlier that numbers are immutable.

![7](/images/python3-2/7.png)

Since we know that numbers are immutable so both  __X__  and  __Y__  have the same id and as well as same value so both  __==__  and  __is__ are returning __TRUE__.

![8](/images/python3-2/8.png)

Since dictionaries are mutable. So even though both  __X__  and  __Y__  have same values their Id’s are different. Therefore, __X  is  Y__  returns  __False__  here but  __X  ==  Y__  is returning __True__.

## Loops in python

Now let’s learn about Loops in Python. Basically, Python has 2 types of loop. One is  __WHILE__  loop and other is  __FOR__  loop.

![9](/images/python3-2/9.png)

This is a simple implementation of  __While__  loop. What while loop does it that it checks for the condition and if it is true it executes the suite of code and after that, it again checks the code and runs the suite until the condition become false.

__For__  loop is little different. It iterates over the objects.

![10](/images/python3-2/10.png)

![11](/images/python3-2/11.png)

lines.txt

What  __for__  loop is doing that it is iterating over the objects till the iterator is out of stuff to iterate. The line object takes each line and prints it. Here fh_.readlines()_  reads each line until the end of the file.

![12](/images/python3-2/12.png)

In a nutshell,  __Range__  function generates a list of numbers, which is generally used to iterate over using for loop.

I will be talking about other iterators in upcoming write-ups. Thanks for reading.