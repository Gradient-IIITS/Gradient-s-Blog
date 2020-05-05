---
title: "Through Python3 (Day 1)"
date: 2019-02-15T00:18:00+05:30
draft: false
toc: true
mathjax: false
author: Krishna Kumar Dey
tags: [ "python", "beginner"]
---

# Through Python3 (Day 1)

Thanks for joining us! I am Krishna and I will be your host for this blog post. This blog post will be guiding you to learn basics of **Python**.

> A little girl goes into a pet show and asks for a wabbit. The shop keeper looks down at her, smiles and says:
“Would you like a lovely fluffy little white rabbit, or a cutesy wootesly little brown rabbit?”
“Actually”, says the little girl, “I don’t think my python would notice.”

<cite> —Nick Leaton, Wed, 04 Dec 1996 </cite>


# Python

Python is an Object-Oriented Programming Language. Everything in Python is an object, i.e. variable or functions or even the whole code.

Acc. to [Wikipedia](https://www.wikipedia.org), Python is an interpreted, high-level, general-purpose programming language. Created by Guido van Rossum and first released in 1991, Python has a design philosophy that emphasizes code readability, notably using significant whitespace. It provides constructs that enable clear programming on both small and large scales


## Variables
So, Let’s learn about variables. What are variables in Python?  
Let,

` X = 30 `

So here X is a variable. X can be anything like

` X = “Krishna” `

Or
 
` X = 30.5 `

Here X is referring to a value of 30.5. But what exactly X is.  

X is an instance of  __int__ Class. How can we say that it’s an instance of a class int? For that, we can use the following command -

` type(Variable_Name) `

![1](/images/python3-1/1.png)

## Objects
Now  let us learn about objects. As I have said earlier everything is an object in Python. But what is an object? An object is an instance of a class. Here as we can see X is variable which is referring to a class __int__.

## Mutable / Immutable
Now let’s talk about  __mutable__  and  __Immutable__. So, what is meant by being mutable? It means that they change values. And Immutable are those who can’t change values. How we will find out whether a class is mutable or immutable.

This can be done using - 

` id(variable_name) `

Id uniquely identifies an instance of an object.

![2](/images/python3-1/2.png)

As we can see here the values changed that means that X is Immutable. But now, here we changed the value of X from 30 to 50. So, we changed it. No, we referenced to another object. Initially, we were referencing an object 30 later we referenced to an object 50.

![3](/images/python3-1/3.png)

Now if you see the id of X changed to the previous id as we changed the reference back to 30. From this, we can say that  __Numbers are Immutable__. Other Immutable data-types are  __Strings, tuple__ etc.

Some of the Mutable data-types are  __Lists, Dictionaries__  etc.

![4](/images/python3-1/4.png)

Here we can see that  __id__ didn’t change. We will learn in detail about these in upcoming days.