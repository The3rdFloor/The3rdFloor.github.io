---
layout: post
title: "A Gentle Introduction To Python"
date: 2017-11-19 10:00 -0500
categories: 
---

This post is a tutorial that will go from a basic introduction to
programming, and finish off with writing a simple ORF finder. If you do 
not know what that is, we will get there.

It is becoming increasingly important in biology to have an
understanding of computational tools. They are appearing everywehere and
are necessary to analyze data on the scale that biologists are looking 
at now.

I am writing this tutorial to be run [here][online-env-1] or [here][online-env-2].
All code in this tutorial _should_ work on both sites. To run the code,
type it in and hit either ```Run``` or ```Execute```, depending on the 
site you decided to use.

If you a ```1337 h@x0r```, feel free to use any environment that you are 
comfortable with to write and run this code.

___
# Part 1: Introduction to Programming

Learning to program can often be intimidating, but it really boils down
to only a few relatively simple concepts, which when combined in unique
ways can perform complex tasks! While other concepts exist, I would argue
that there are three major categories that most of these concepts fit
into: variables, operations, and control flow. In brief, these mean how
we store information, how we manipulate information, and how we tell the
computer which and when to perform operations on variables. With this in
mind, we will get started with writing your first program, then going
through applying each of these three concepts in Python. 


It is tradition in the world of computer geeks to always write the
famous "Hello, world!" program when you learn a new language, so we will
start with that. Enter the following code into your editor, then hit
```Run``` and pat yourself on the back, with the knowledge that you are
now a programmer.

{% highlight python %}
print("Hello, World!")
{% endhighlight %}

If you get everything right, your computer printed out ```"Hello, World!"```.
Great work! Now let's get into the meat of programming, now that we know
how to write a program! 

# Variables
A variable is like a box, it stores some item for you. This item can be
all sorts of different things, including letters, numbers, or even DNA
sequences. Below are a few examples:

{% highlight python %}
an_integer = 42
a_float = 3.14
a_string = "A series of symbols and letters"
another_string = 'Could be written using single quotes in Python'
{% endhighlight %}

You will notice that each variable created in the same way. First, it
has a name, followed by an '=' sign, followed by the value. We are 
'binding' this value to the name. Finally, each variable has a 'type', 
which describes what the data is. An 'integer' is, well, an integer, a 
'float', short for 'floating point number', is a number with decimal
values, and a string is just a series of symbols. We wil luse a string
to store a DNA sequence later. Whenever you have a piece of information
that you want to store and use later, you should put it in a variable.
Not only does this make it convenient to access later, it makes it 
easier to remember what the data you're storing is! Consider the two
snippets of code below:

{% highlight python %}
print(3.14159)
{% endhighlight %}
as oppose to something like this:
{% highlight python %}
pi = 3.14159
print(pi)
{% endhighlight %}

Both of these code snippets will do the exact same thing, but in the
second, you know exactly what is being printed, the value of Pi!

What if we have a collection of items that we want to store? Python has
the answer! We can use lists. In fact, a string is effectively a list,
but we won't go much into that. Below are some examples of lists.

{% highlight python %}
empty_list = []
list_of_numbers = [1, 2, 3, 4]
{% endhighlight %}

We can access each item by using the item's index, starting from 0. Take
careful note of this, it can lead to mistakes easily. 

{% highlight python %}
string_list = ["item1", "item2", "item3"]
print( string_list[0] )
print( string_list[2] )
{% endhighlight %}

This should print the following if you run it:

```
item1
item3
```

We can also get a 'slice' of a list like so:

{% highlight python %}
a_list = [1,2,3,4]
print( a_list[1:3] )
{% endhighlight %}

Notice that this prints items starting from index 1 (i.e. the second
item in the list) up to, but not including, the item at index 3 (i.e. 
the fourth item in the list).

As a final note, strings can accessed in the same way. For example, we 
could get the first three letters of a DNA sequence like this:

{% highlight python %}
dna_seq = "ATCGTCGTGATGCATGCA"
print( dna_seq[0:3] )
{% endhighlight %}

# Operations
Variables are great and all, but they aren't particularly useful if we
can't do anything with them. This brings us to operations, the small
manipulations we can perform on variables and other data. These include
things like addition, subtraction, and multiplication.

{% highlight python %}
print(1 + 2)
some_number = 1.2
some_other_number = 3.4
print(some_number + some_other_number)
a_new_number = some_number * some_other_number
print(a_new_number)
{% endhighlight %}

Python is even smart enough to imply what something like addition or 
multiplication could mean on a string!

{% highlight python %}
last_name = "Deckard"
first_name = "Rick"
print(first_name + " " + last_name) 	# Print out full name in order
print(5 * last_name) 			# Print last_name 5 times
{% endhighlight %}
The first print adds ```first_name``` to a space to ```last_name``` and
prints it. The second prints ```last_name``` 5 times. 

I also (rather
sneakily) introduced a new seemingly minor, but VERY important idea
here: comments! In Python, if you type a '#', everything following it on
the same line is not considered part of the code. This is extremely
useful to help you organize and annotate code. It is very easy to
revisit code and completely forget what it does if you have not left
comments. 

___
# Part 2: Building an ORF Finder

![Image of Phi X Phage, sequenced by Sanger in 1974](/assets/phi_x_phage.jpg)

___
# Further Reading

[online-env-1]: https://repl.it/languages/python3
[online-env-2]: https://www.tutorialspoint.com/execute_python_online.php
