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

This should print ```ATC```.

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

Finally, many things in Python have different functions associated with
them. For the sake of this tutorial, we will consider these operations.
Some of the most useful functions are functions that work on strings.
The code below illustrates a simple program for getting the GC content
of a DNA sequence using some of the functions associated with genes.

{% highlight python %}
dna_seq = "ATCGATCGTACGTACGGTCAGTACGTCAGCTACGTGCATGCATGACGT"
seq_length = len(dna_seq)
gc_count = dna_seq.count("G") + dna_seq.count("C")
print("The percent GC content of the sequence is:")
print( gc_count/seq_length )
{% endhighlight %}

This should print the following:
```
The percent GC content of the sequence is:
0.5208333333333334
```

Another useful function is ```.index()```. This will get the index of the
first occurence of something in your string. For example:

{% highlight python %}
dna_seq = "TCTGATGCAAGCATATAAGCGCAA"
print( dna_seq.index("ATG") )
{% endhighlight %}

This should print ```4``` if everything is correct. While quite small, 
this deceptively simple program is capable of finding the first start
codon in a DNA sequence!

# Flow Control
We have now seen how we can store and manipulate data, but our programs 
have all been linear, thus far. That is, they go step by step and always
do the exact same thing, no matter how the data changes! This doesn't 
offer a lot of flexibility. Enter flow control.

Flow control is the term referring to how we can make programs behave 
differently depending on the conditions the program is run under. We
will look at three ways in which we can change the flow of a program: if
statements, for loops, and while loops.

#### The If Statement

An if statement can be used when we want the program to do one thing if 
something is true, or another if it is not. The most basic if statement
is called an if-else. An example is below:

{% highlight python %}
dna_seq = "ATGCTGTCGGCTAGGACTCGCTAGTAC"
if ( dna_seq[0:3] == "ATG" ):
	print("This sequence begins with a start codon!")
else:
	print("This sequence does not begin with a start codon.")
{% endhighlight %}

You should see ```This sequence begins with a start codon!``` printed to
your screen when you run this code. Try changing the DNA sequence by 
changing the first line to this:
{% highlight python %}
dna_seq = "TCACTGTCGGCTAGGACTCGCTAGTAC"
{% endhighlight %}
Notice that the output has changed?
No? It hasn't? Then you haven't copied the code correctly, try again.

Before we go on, let's take a look at one new thing that shows up here:
code blocks. Code blocks are how code is organized into logical 
sections. *These are very important*! The computer uses code blocks to
determine what code to run as part of an if statement, a loop, or a
function (something we won't be covering). A code block consists of all
the code that is indented by a tab. Everything within the tabbed section
is part of that block. It is standard to use 4 spaces as a tab in
Python. 

If statements can also be made more complex, allowing us to handle
situations where we have more than one option we may want to take. Below
we have an example using an ```elif```, short for 'else if'.

{% highlight python %}
codon = "TAA"
if ( codon == "ATG" ):
	print("This is a start codon.")
elif ( codon in ["TAA", "TAG", "TGA"] ):
	print(" This is a stop codon.")
else:
	print("This is neither a stop nor a start codon.")
{% endhighlight %}

This example will print ```This is a stop codon.```
I also introduced a useful operator here; the ```in``` operator. This is
useful for determining if something is contained in a collection of
items. 

#### The For Loop

One of the most powerful ways of controlling program flow is by way of a
loop. This allows you to use the same bit of code many times over again,
which can save a lot of time for a few obvious reasons. The idea behind 
a for loop is that it incrementally changes some variable that you want
to manipulate with each iteration of the loop. In many languages, this
is usually a number. In Python specifically, this can be done like so:

{% highlight python %}
for i in range(0, 10):
	print(i)
{% endhighlight %}

There are a few things to notice about this snippet of code. Firstly, 
notice that it uses code blocks in a similar way to the if statement.
The second thing to notice is the ```i```. This is a variable that will
store some value for each iteration of the loop. In this case, Python
will generate a range from 0 to 10, not including 10, and with each 
round of the loop, ```i``` will take on one of those values. Try running
this code and take note of what happens. 

But that's not all ```for``` loops can do in Python! They can loop over
almost anything that has a logical iterable *feeling* to it. For
example, the following snippet will iterate over each letter in a sequence and 
print any sybol that is not a valid nucleotide (i.e. is one
of A, T, C, or G).

{% highlight python %}
dna_seq = "ATCGCTGACTGCATGCQACTGCATGCAHCATGCAGCY"
valid_dna = "ATCG"
for symbol in dna_seq:
	if not ( symbol in valid_dna ):
		print(symbol)
{% endhighlight %}

There are a few new things that I have introduced here. First of all,
notice the use of ```not```. This will check the condition in the if
statement, then take the opposite. So if ```symbol``` is in ```valid_dna```,
then we do not want to print it. The second thing to notice is that the
code blocks were nested. What that means is that we can put loops or if
statements within one another!

#### The While Loop

And now we come to our final tool for controlling the flow of a program,
and the final concept we will tackle before we get into building an ORF
finder; the while loop. 

A while loop combined a condition, like in if statements, with the 
ability to loop. At the start of each iteration, it will check to see if
a condition is met. If it is, then it will run through the loop, rinse,
and repeat. The example below will decrement ```counter``` by 1 until it hits
0, then it will stop.

{% highlight python %}
counter = 10
while ( counter > 0 ):
	print(counter)
	counter = counter - 1
print("Done.")
{% endhighlight %}

We now have all of the tools (and a few extras) that we need to start
building an ORF finder! From here on out, this post will be stepping
through and building the ORF finder up, bit by bit. 

___
# Part 2: Building an ORF Finder

I would like to introduce you to Phy X Phage, the first DNA based 
organism to be sequenced (in 1974 by Sanger et al.)

![Image of Phi X Phage, sequenced by Sanger in 1974](/assets/phi_x_phage.jpg)
(Image courtesy of Dr. Doxey)

I would now like to introduce you to its genome:

```
>gi|9626372|ref|NC_001422.1| Enterobacteria phage phiX174, complete genome
GAGTTTTATCGCTTCCATGACGCAGAAGTTAACACTTTCGGATATTTCTGATGAGTCGAAAAATTATCTTGATAAAGCAGGAATTACTACTGCTTGTTTACGAATTAAATCGAAGTGGACTGCTGGCGGAAAATGAGAAAATTCGACCTATCCTTGCGCAGCTCGAGAAGCTCTTACTTTGCGACCTTTCGCCATCAACTAACGATTCTGTCAAAAACTGACGCGTTGGATGAGGAGAAGTGGCTTAATATGCTTGGCACGTTCGTCAAGGACTGGTTTAGATATGAGTCACATTTTGTTCATGGTAGAGATTCTCTTGTTGACATTTTAAAAGAGCGTGGATTACTATCTGAGTCCGATGCTGTTCAACCACTAATAGGTAAGAAATCATGAGTCAAGTTACTGAACAATCCGTACGTTTCCAGACCGCTTTGGCCTCTATTAAGCTCATTCAGGCTTCTGCCGTTTTGGATTTAACCGAAGATGATTTCGATTTTCTGACGAGTAACAAAGTTTGGATTGCTACTGACCGCTCTCGTGCTCGTCGCTGCGTTGAGGCTTGCGTTTATGGTACGCTGGACTTTGTGGGATACCCTCGCTTTCCTGCTCCTGTTGAGTTTATTGCTGCCGTCATTGCTTATTATGTTCATCCCGTCAACATTCAAACGGCCTGTCTCATCATGGAAGGCGCTGAATTTACGGAAAACATTATTAATGGCGTCGAGCGTCCGGTTAAAGCCGCTGAATTGTTCGCGTTTACCTTGCGTGTACGCGCAGGAAACACTGACGTTCTTACTGACGCAGAAGAAAACGTGCGTCAAAAATTACGTGCGGAAGGAGTGATGTAATGTCTAAAGGTAAAAAACGTTCTGGCGCTCGCCCTGGTCGTCCGCAGCCGTTGCGAGGTACTAAAGGCAAGCGTAAAGGCGCTCGTCTTTGGTATGTAGGTGGTCAACAATTTTAATTGCAGGGGCTTCGGCCCCTTACTTGAGGATAAATTATGTCTAATATTCAAACTGGCGCCGAGCGTATGCCGCATGACCTTTCCCATCTTGGCTTCCTTGCTGGTCAGATTGGTCGTCTTATTACCATTTCAACTACTCCGGTTATCGCTGGCGACTCCTTCGAGATGGACGCCGTTGGCGCTCTCCGTCTTTCTCCATTGCGTCGTGGCCTTGCTATTGACTCTACTGTAGACATTTTTACTTTTTATGTCCCTCATCGTCACGTTTATGGTGAACAGTGGATTAAGTTCATGAAGGATGGTGTTAATGCCACTCCTCTCCCGACTGTTAACACTACTGGTTATATTGACCATGCCGCTTTTCTTGGCACGATTAACCCTGATACCAATAAAATCCCTAAGCATTTGTTTCAGGGTTATTTGAATATCTATAACAACTATTTTAAAGCGCCGTGGATGCCTGACCGTACCGAGGCTAACCCTAATGAGCTTAATCAAGATGATGCTCGTTATGGTTTCCGTTGCTGCCATCTCAAAAACATTTGGACTGCTCCGCTTCCTCCTGAGACTGAGCTTTCTCGCCAAATGACGACTTCTACCACATCTATTGACATTATGGGTCTGCAAGCTGCTTATGCTAATTTGCATACTGACCAAGAACGTGATTACTTCATGCAGCGTTACCATGATGTTATTTCTTCATTTGGAGGTAAAACCTCTTATGACGCTGACAACCGTCCTTTACTTGTCATGCGCTCTAATCTCTGGGCATCTGGCTATGATGTTGATGGAACTGACCAAACGTCGTTAGGCCAGTTTTCTGGTCGTGTTCAACAGACCTATAAACATTCTGTGCCGCGTTTCTTTGTTCCTGAGCATGGCACTATGTTTACTCTTGCGCTTGTTCGTTTTCCGCCTACTGCGACTAAAGAGATTCAGTACCTTAACGCTAAAGGTGCTTTGACTTATACCGATATTGCTGGCGACCCTGTTTTGTATGGCAACTTGCCGCCGCGTGAAATTTCTATGAAGGATGTTTTCCGTTCTGGTGATTCGTCTAAGAAGTTTAAGATTGCTGAGGGTCAGTGGTATCGTTATGCGCCTTCGTATGTTTCTCCTGCTTATCACCTTCTTGAAGGCTTCCCATTCATTCAGGAACCGCCTTCTGGTGATTTGCAAGAACGCGTACTTATTCGCCACCATGATTATGACCAGTGTTTCCAGTCCGTTCAGTTGTTGCAGTGGAATAGTCAGGTTAAATTTAATGTGACCGTTTATCGCAATCTGCCGACCACTCGCGATTCAATCATGACTTCGTGATAAAAGATTGAGTGTGAGGTTATAACGCCGAAGCGGTAAAAATTTTAATTTTTGCCGCTGAGGGGTTGACCAAGCGAAGCGCGGTAGGTTTTCTGCTTAGGAGTTTAATCATGTTTCAGACTTTTATTTCTCGCCATAATTCAAACTTTTTTTCTGATAAGCTGGTTCTCACTTCTGTTACTCCAGCTTCTTCGGCACCTGTTTTACAGACACCTAAAGCTACATCGTCAACGTTATATTTTGATAGTTTGACGGTTAATGCTGGTAATGGTGGTTTTCTTCATTGCATTCAGATGGATACATCTGTCAACGCCGCTAATCAGGTTGTTTCTGTTGGTGCTGATATTGCTTTTGATGCCGACCCTAAATTTTTTGCCTGTTTGGTTCGCTTTGAGTCTTCTTCGGTTCCGACTACCCTCCCGACTGCCTATGATGTTTATCCTTTGAATGGTCGCCATGATGGTGGTTATTATACCGTCAAGGACTGTGTGACTATTGACGTCCTTCCCCGTACGCCGGGCAATAACGTTTATGTTGGTTTCATGGTTTGGTCTAACTTTACCGCTACTAAATGCCGCGGATTGGTTTCGCTGAATCAGGTTATTAAAGAGATTATTTGTCTCCAGCCACTTAAGTGAGGTGATTTATGTTTGGTGCTATTGCTGGCGGTATTGCTTCTGCTCTTGCTGGTGGCGCCATGTCTAAATTGTTTGGAGGCGGTCAAAAAGCCGCCTCCGGTGGCATTCAAGGTGATGTGCTTGCTACCGATAACAATACTGTAGGCATGGGTGATGCTGGTATTAAATCTGCCATTCAAGGCTCTAATGTTCCTAACCCTGATGAGGCCGCCCCTAGTTTTGTTTCTGGTGCTATGGCTAAAGCTGGTAAAGGACTTCTTGAAGGTACGTTGCAGGCTGGCACTTCTGCCGTTTCTGATAAGTTGCTTGATTTGGTTGGACTTGGTGGCAAGTCTGCCGCTGATAAAGGAAAGGATACTCGTGATTATCTTGCTGCTGCATTTCCTGAGCTTAATGCTTGGGAGCGTGCTGGTGCTGATGCTTCCTCTGCTGGTATGGTTGACGCCGGATTTGAGAATCAAAAAGAGCTTACTAAAATGCAACTGGACAATCAGAAAGAGATTGCCGAGATGCAAAATGAGACTCAAAAAGAGATTGCTGGCATTCAGTCGGCGACTTCACGCCAGAATACGAAAGACCAGGTATATGCACAAAATGAGATGCTTGCTTATCAACAGAAGGAGTCTACTGCTCGCGTTGCGTCTATTATGGAAAACACCAATCTTTCCAAGCAACAGCAGGTTTCCGAGATTATGCGCCAAATGCTTACTCAAGCTCAAACGGCTGGTCAGTATTTTACCAATGACCAAATCAAAGAAATGACTCGCAAGGTTAGTGCTGAGGTTGACTTAGTTCATCAGCAAACGCAGAATCAGCGGTATGGCTCTTCTCATATTGGCGCTACTGCAAAGGATATTTCTAATGTCGTCACTGATGCTGCTTCTGGTGTGGTTGATATTTTTCATGGTATTGATAAAGCTGTTGCCGATACTTGGAACAATTTCTGGAAAGACGGTAAAGCTGATGGTATTGGCTCTAATTTGTCTAGGAAATAACCGTCAGGATTGACACCCTCCCAATTGTATGTTTTCATGCCTCCAAATCTTGGAGGCTTTTTTATGGTTCGTTCTTATTACCCTTCTGAATGTCACGCTGATTATTTTGACTTTGAGCGTATCGAGGCTCTTAAACCTGCTATTGAGGCTTGTGGCATTTCTACTCTTTCTCAATCCCCAATGCTTGGCTTCCATAAGCAGATGGATAACCGCATCAAGCTCTTGGAAGAGATTCTGTCTTTTCGTATGCAGGGCGTTGAGTTCGATAATGGTGATATGTATGTTGACGGCCATAAGGCTGCTTCTGACGTTCGTGATGAGTTTGTATCTGTTACTGAGAAGTTAATGGATGAATTGGCACAATGCTACAATGTGCTCCCCCAACTTGATATTAATAACACTATAGACCACCGCCCCGAAGGGGACGAAAAATGGTTTTTAGAGAACGAGAAGACGGTTACGCAGTTTTGCCGCAAGCTGGCTGCTGAACGCCCTCTTAAGGATATTCGCGATGAGTATAATTACCCCAAAAAGAAAGGTATTAAGGATGAGTGTTCAAGATTGCTGGAGGCCTCCACTATGAAATCGCGTAGAGGCTTTGCTATTCAGCGTTTGATGAATGCAATGCGACAGGCTCATGCTGATGGTTGGTTTATCGTTTTTGACACTCTCACGTTGGCTGACGACCGATTAGAGGCGTTTTATGATAATCCCAATGCTTTGCGTGACTATTTTCGTGATATTGGTCGTATGGTTCTTGCTGCCGAGGGTCGCAAGGCTAATGATTCACACGCCGACTGCTATCAGTATTTTTGTGTGCCTGAGTATGGTACAGCTAATGGCCGTCTTCATTTCCATGCGGTGCACTTTATGCGGACACTTCCTACAGGTAGCGTTGACCCTAATTTTGGTCGTCGGGTACGCAATCGCCGCCAGTTAAATAGCTTGCAAAATACGTGGCCTTATGGTTACAGTATGCCCATCGCAGTTCGCTACACGCAGGACGCTTTTTCACGTTCTGGTTGGTTGTGGCCTGTTGATGCTAAAGGTGAGCCGCTTAAAGCTACCAGTTATATGGCTGTTGGTTTCTATGTGGCTAAATACGTTAACAAAAAGTCAGATATGGACCTTGCTGCTAAAGGTCTAGGAGCTAAAGAATGGAACAACTCACTAAAAACCAAGCTGTCGCTACTTCCCAAGAAGCTGTTCAGAATCAGAATGAGCCGCAACTTCGGGATGAAAATGCTCACAATGACAAATCTGTCCACGGAGTGCTTAATCCAACTTACCAAGCTGGGTTACGACGCGACGCCGTTCAACCAGATATTGAAGCAGAACGCAAAAAGAGAGATGAGATTGAGGCTGGGAAAAGTTACTGTAGCCGACGTTTTGGCGGCGCAACCTGTGACGACAAATCTGCTCAAATTTATGCGCGCTTCGATAAAAATGATTGGCGTATCCAACCTGCA
```

It is quite small! Only about 5kb, encoding only 11 proteins. But this
is why its a perfect genome to start working with! 

To start off, we will copy the sequence into a variable. In general, you
would not just copy the sequence in like this, you would use [Pythons's file I/O][file-io],
but for the sake of simplicity, just copy it into a variable like so:

{% highlight python %}
phi_genome = """
GAGTTTTATCGCTTCCATGACGCAGAAGTTAACACTTTCGGATATTTCTGATGAGTCGAAAAATTATCTTGATAAAGCAGGAATTACTACTGCTTGTTTACGAATTAAATCGAAGTGGACTGCTGGCGGAAAATGAGAAAATTCGACCTATCCTTGCGCAGCTCGAGAAGCTCTTACTTTGCGACCTTTCGCCATCAACTAACGATTCTGTCAAAAACTGACGCGTTGGATGAGGAGAAGTGGCTTAATATGCTTGGCACGTTCGTCAAGGACTGGTTTAGATATGAGTCACATTTTGTTCATGGTAGAGATTCTCTTGTTGACATTTTAAAAGAGCGTGGATTACTATCTGAGTCCGATGCTGTTCAACCACTAATAGGTAAGAAATCATGAGTCAAGTTACTGAACAATCCGTACGTTTCCAGACCGCTTTGGCCTCTATTAAGCTCATTCAGGCTTCTGCCGTTTTGGATTTAACCGAAGATGATTTCGATTTTCTGACGAGTAACAAAGTTTGGATTGCTACTGACCGCTCTCGTGCTCGTCGCTGCGTTGAGGCTTGCGTTTATGGTACGCTGGACTTTGTGGGATACCCTCGCTTTCCTGCTCCTGTTGAGTTTATTGCTGCCGTCATTGCTTATTATGTTCATCCCGTCAACATTCAAACGGCCTGTCTCATCATGGAAGGCGCTGAATTTACGGAAAACATTATTAATGGCGTCGAGCGTCCGGTTAAAGCCGCTGAATTGTTCGCGTTTACCTTGCGTGTACGCGCAGGAAACACTGACGTTCTTACTGACGCAGAAGAAAACGTGCGTCAAAAATTACGTGCGGAAGGAGTGATGTAATGTCTAAAGGTAAAAAACGTTCTGGCGCTCGCCCTGGTCGTCCGCAGCCGTTGCGAGGTACTAAAGGCAAGCGTAAAGGCGCTCGTCTTTGGTATGTAGGTGGTCAACAATTTTAATTGCAGGGGCTTCGGCCCCTTACTTGAGGATAAATTATGTCTAATATTCAAACTGGCGCCGAGCGTATGCCGCATGACCTTTCCCATCTTGGCTTCCTTGCTGGTCAGATTGGTCGTCTTATTACCATTTCAACTACTCCGGTTATCGCTGGCGACTCCTTCGAGATGGACGCCGTTGGCGCTCTCCGTCTTTCTCCATTGCGTCGTGGCCTTGCTATTGACTCTACTGTAGACATTTTTACTTTTTATGTCCCTCATCGTCACGTTTATGGTGAACAGTGGATTAAGTTCATGAAGGATGGTGTTAATGCCACTCCTCTCCCGACTGTTAACACTACTGGTTATATTGACCATGCCGCTTTTCTTGGCACGATTAACCCTGATACCAATAAAATCCCTAAGCATTTGTTTCAGGGTTATTTGAATATCTATAACAACTATTTTAAAGCGCCGTGGATGCCTGACCGTACCGAGGCTAACCCTAATGAGCTTAATCAAGATGATGCTCGTTATGGTTTCCGTTGCTGCCATCTCAAAAACATTTGGACTGCTCCGCTTCCTCCTGAGACTGAGCTTTCTCGCCAAATGACGACTTCTACCACATCTATTGACATTATGGGTCTGCAAGCTGCTTATGCTAATTTGCATACTGACCAAGAACGTGATTACTTCATGCAGCGTTACCATGATGTTATTTCTTCATTTGGAGGTAAAACCTCTTATGACGCTGACAACCGTCCTTTACTTGTCATGCGCTCTAATCTCTGGGCATCTGGCTATGATGTTGATGGAACTGACCAAACGTCGTTAGGCCAGTTTTCTGGTCGTGTTCAACAGACCTATAAACATTCTGTGCCGCGTTTCTTTGTTCCTGAGCATGGCACTATGTTTACTCTTGCGCTTGTTCGTTTTCCGCCTACTGCGACTAAAGAGATTCAGTACCTTAACGCTAAAGGTGCTTTGACTTATACCGATATTGCTGGCGACCCTGTTTTGTATGGCAACTTGCCGCCGCGTGAAATTTCTATGAAGGATGTTTTCCGTTCTGGTGATTCGTCTAAGAAGTTTAAGATTGCTGAGGGTCAGTGGTATCGTTATGCGCCTTCGTATGTTTCTCCTGCTTATCACCTTCTTGAAGGCTTCCCATTCATTCAGGAACCGCCTTCTGGTGATTTGCAAGAACGCGTACTTATTCGCCACCATGATTATGACCAGTGTTTCCAGTCCGTTCAGTTGTTGCAGTGGAATAGTCAGGTTAAATTTAATGTGACCGTTTATCGCAATCTGCCGACCACTCGCGATTCAATCATGACTTCGTGATAAAAGATTGAGTGTGAGGTTATAACGCCGAAGCGGTAAAAATTTTAATTTTTGCCGCTGAGGGGTTGACCAAGCGAAGCGCGGTAGGTTTTCTGCTTAGGAGTTTAATCATGTTTCAGACTTTTATTTCTCGCCATAATTCAAACTTTTTTTCTGATAAGCTGGTTCTCACTTCTGTTACTCCAGCTTCTTCGGCACCTGTTTTACAGACACCTAAAGCTACATCGTCAACGTTATATTTTGATAGTTTGACGGTTAATGCTGGTAATGGTGGTTTTCTTCATTGCATTCAGATGGATACATCTGTCAACGCCGCTAATCAGGTTGTTTCTGTTGGTGCTGATATTGCTTTTGATGCCGACCCTAAATTTTTTGCCTGTTTGGTTCGCTTTGAGTCTTCTTCGGTTCCGACTACCCTCCCGACTGCCTATGATGTTTATCCTTTGAATGGTCGCCATGATGGTGGTTATTATACCGTCAAGGACTGTGTGACTATTGACGTCCTTCCCCGTACGCCGGGCAATAACGTTTATGTTGGTTTCATGGTTTGGTCTAACTTTACCGCTACTAAATGCCGCGGATTGGTTTCGCTGAATCAGGTTATTAAAGAGATTATTTGTCTCCAGCCACTTAAGTGAGGTGATTTATGTTTGGTGCTATTGCTGGCGGTATTGCTTCTGCTCTTGCTGGTGGCGCCATGTCTAAATTGTTTGGAGGCGGTCAAAAAGCCGCCTCCGGTGGCATTCAAGGTGATGTGCTTGCTACCGATAACAATACTGTAGGCATGGGTGATGCTGGTATTAAATCTGCCATTCAAGGCTCTAATGTTCCTAACCCTGATGAGGCCGCCCCTAGTTTTGTTTCTGGTGCTATGGCTAAAGCTGGTAAAGGACTTCTTGAAGGTACGTTGCAGGCTGGCACTTCTGCCGTTTCTGATAAGTTGCTTGATTTGGTTGGACTTGGTGGCAAGTCTGCCGCTGATAAAGGAAAGGATACTCGTGATTATCTTGCTGCTGCATTTCCTGAGCTTAATGCTTGGGAGCGTGCTGGTGCTGATGCTTCCTCTGCTGGTATGGTTGACGCCGGATTTGAGAATCAAAAAGAGCTTACTAAAATGCAACTGGACAATCAGAAAGAGATTGCCGAGATGCAAAATGAGACTCAAAAAGAGATTGCTGGCATTCAGTCGGCGACTTCACGCCAGAATACGAAAGACCAGGTATATGCACAAAATGAGATGCTTGCTTATCAACAGAAGGAGTCTACTGCTCGCGTTGCGTCTATTATGGAAAACACCAATCTTTCCAAGCAACAGCAGGTTTCCGAGATTATGCGCCAAATGCTTACTCAAGCTCAAACGGCTGGTCAGTATTTTACCAATGACCAAATCAAAGAAATGACTCGCAAGGTTAGTGCTGAGGTTGACTTAGTTCATCAGCAAACGCAGAATCAGCGGTATGGCTCTTCTCATATTGGCGCTACTGCAAAGGATATTTCTAATGTCGTCACTGATGCTGCTTCTGGTGTGGTTGATATTTTTCATGGTATTGATAAAGCTGTTGCCGATACTTGGAACAATTTCTGGAAAGACGGTAAAGCTGATGGTATTGGCTCTAATTTGTCTAGGAAATAACCGTCAGGATTGACACCCTCCCAATTGTATGTTTTCATGCCTCCAAATCTTGGAGGCTTTTTTATGGTTCGTTCTTATTACCCTTCTGAATGTCACGCTGATTATTTTGACTTTGAGCGTATCGAGGCTCTTAAACCTGCTATTGAGGCTTGTGGCATTTCTACTCTTTCTCAATCCCCAATGCTTGGCTTCCATAAGCAGATGGATAACCGCATCAAGCTCTTGGAAGAGATTCTGTCTTTTCGTATGCAGGGCGTTGAGTTCGATAATGGTGATATGTATGTTGACGGCCATAAGGCTGCTTCTGACGTTCGTGATGAGTTTGTATCTGTTACTGAGAAGTTAATGGATGAATTGGCACAATGCTACAATGTGCTCCCCCAACTTGATATTAATAACACTATAGACCACCGCCCCGAAGGGGACGAAAAATGGTTTTTAGAGAACGAGAAGACGGTTACGCAGTTTTGCCGCAAGCTGGCTGCTGAACGCCCTCTTAAGGATATTCGCGATGAGTATAATTACCCCAAAAAGAAAGGTATTAAGGATGAGTGTTCAAGATTGCTGGAGGCCTCCACTATGAAATCGCGTAGAGGCTTTGCTATTCAGCGTTTGATGAATGCAATGCGACAGGCTCATGCTGATGGTTGGTTTATCGTTTTTGACACTCTCACGTTGGCTGACGACCGATTAGAGGCGTTTTATGATAATCCCAATGCTTTGCGTGACTATTTTCGTGATATTGGTCGTATGGTTCTTGCTGCCGAGGGTCGCAAGGCTAATGATTCACACGCCGACTGCTATCAGTATTTTTGTGTGCCTGAGTATGGTACAGCTAATGGCCGTCTTCATTTCCATGCGGTGCACTTTATGCGGACACTTCCTACAGGTAGCGTTGACCCTAATTTTGGTCGTCGGGTACGCAATCGCCGCCAGTTAAATAGCTTGCAAAATACGTGGCCTTATGGTTACAGTATGCCCATCGCAGTTCGCTACACGCAGGACGCTTTTTCACGTTCTGGTTGGTTGTGGCCTGTTGATGCTAAAGGTGAGCCGCTTAAAGCTACCAGTTATATGGCTGTTGGTTTCTATGTGGCTAAATACGTTAACAAAAAGTCAGATATGGACCTTGCTGCTAAAGGTCTAGGAGCTAAAGAATGGAACAACTCACTAAAAACCAAGCTGTCGCTACTTCCCAAGAAGCTGTTCAGAATCAGAATGAGCCGCAACTTCGGGATGAAAATGCTCACAATGACAAATCTGTCCACGGAGTGCTTAATCCAACTTACCAAGCTGGGTTACGACGCGACGCCGTTCAACCAGATATTGAAGCAGAACGCAAAAAGAGAGATGAGATTGAGGCTGGGAAAAGTTACTGTAGCCGACGTTTTGGCGGCGCAACCTGTGACGACAAATCTGCTCAAATTTATGCGCGCTTCGATAAAAATGATTGGCGTATCCAACCTGCA
"""
{% endhighlight %}

The triple quotes here are just a way to represent a string that is very
large and that could span multiple lines.

If you do want to try doing this using file I/O, or just to make a copy
and paste easier, the fasta file is available [here](/assets/phi-x-genome.fasta).

Now that we have a sequence in place, let's plan out our program. 
Finding an ORF can be a relatively complex task, since we have to 
consider both the forward and reverse strand of DNA, we have to consider
whether or not the genome is cyclic, and we need to think about where
the start and stop codons are. But since we are just starting, we will
only consider a few of these aspects for now. I will include a more
complicated ORF finder for you to download and look at in your own time.

To solve this problem, we will use a common algorithmic techniqe called
a 'sliding window'. We will create a window that looks at three nucleotides
at a time and slides along the entire genome. To further simplify this,
we are just going to look for the first sequence, and we won't bother
looking for the start codon, just the stop codon. 

___
# Exercises and Challenges for Practice
- Add the ability to find start codons
- Print out the amino acid sequence of an ORF (Hint: Read up on [dictionaries][python-dict]
and see if you can use them to store codons and their respective [1-letter code][1-letter-code])
- Add the ability to search all 6 reading frames
- Make the ORF finder treat the genome like it's cyclic

___
# Further Reading

[online-env-1]: https://repl.it/languages/python3
[online-env-2]: https://www.tutorialspoint.com/execute_python_online.php
[python-dict]: https://www.tutorialspoint.com/python/python_dictionary.htm
[1-letter-code]: http://www.fao.org/docrep/004/Y2775E/y2775e0e.htm
[file-io]: https://docs.python.org/3.5/tutorial/inputoutput.html#reading-and-writing-files
