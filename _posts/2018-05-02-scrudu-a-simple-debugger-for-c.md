---
layout: posts
title: "Scrúdú: A Simple Debugger for C"
date: 2018-05-02 10:00 -0500
categories: programming tutorials debugging
---

I have been developing a project using the C programming language, and in doing so, I have relearned the frustration
that is C development (at times – C is great). With bugs popping up at every corner, I decided that I needed to look
into creating a framework for unit testing my code. After some research, I found [MinUnit][minunit], a very minimal testing 
framework built into a C header. This got me started on my "journey" to becoming better with testing my code. I 
started to build up a framework that could automatically run tests as I compiled my code so that I knew, with ever
addition to my source, I was not breaking anything.

The idea was to build a unit tester where I could define a function which tested some aspect of code using macro
defined asserts. I could then compile code, and run that function. If the assert passed, then I knew the test was
behaving the way I wanted it to. Thus [unittest][unittest] was born. It worked pretty well, and I slowly added more
and more to it, until it was behaving the way I wanted it to. Then I took a bit of a hiatus from programming in C,
and unittest accumulated some dust.

Upon my return to the world of C recently, I was confronted with the issue of being able to check how well my 
programs were allocating memory. Was everything being freed? How much space was I allocating? Where was it being
allocated? That sort of thing. This, once again, launced me into some research to better understand ways to test
and assess the quality of my code. I dusted off unitttest and started developing [Scrúdú][scrudu], a lightweight testing
framework built mostly on various macros. My plan with this post is to outline, briefly, how I developed this,
how I discovered the power of macros, and how to use [Scrúdú][scrudu].

# A Brief Introduction to Unit Testing

Unit testing is an extrmely powerful methodology for developing code. The idea is to first think of the behaviour
you want from a specific function. For example, imagine that I want to calculate the square of some number, x. 
I first consider what output I would expect from a squaring function, given the input x. I would then write these
tests and the skeleton (i.e. just the signature and a blank return) for my square function. The test would be, in
pseudocode, something like this;
```
if (square(3) == 9)
	print "Success!"
else
	print "Fail!"
```
And my function, for now, would look something like this:
```c
int square(int x) {
	return 0;
}
```

Of course, this would fail, for now. To make things a little more robust, I would likely define a few more
functions, something like this:
```
test( square(3) == 9 )
test( square(0) == 0 )
test( square(1) == 1 )
test( square(-2) == 4 )
```
Again, these should all fail. The finaly step is to slowly build the code up to make these tests all pass. 
In the case of our square function, this is simple and only needs one line of code:
```c
int square(int x) {
	return x*x;
}
```
This will make all of the tests pass (yay!) In practice, it's a little more complicated than that. For
example, maybe we want this to work for imaginary numbers. This would likely mean we need some function
that can parse a string into a number or an imaginary number. This is a new function, which we would 
write more unit tests for. Now we have that working and we realize that some times the user may give
an invalid string as input. We now need to add more unit tests. Then we need to update the function
to work, regardless of if the number is imaginary or real – more tests! This example is, hopefully, enough
to illustrate the iterative process of building up code from simple unit tests. 

# Unit Testing in UnitTest (and now in Scrúdú)

This is where we get into [Scrúdú][scrudu]!

My original code used two key macros to build unit tests. The idea is that the provided source code
file (i.e. the .c file) contained a ```main()``` function where tests could be run. The programmer can write
their tests, as functions, then in main, just run each one successively. 

These tests worked by calling two different macros. The first macro, ```ut_assert```, simply evaluates
some condition. The second macro, ```ut_run```, runs a provided function, which should be the test
function. Let's see how these work with an example, our square example.

Somewhere in the code, we would define our tests, naming them anything we want, like this:
```c
int my_test() {
	return 0;
}
```
We would then use that name to run them, like so:
```c
int main() {
	ut_run( my_test );
	return 0;
}
```
As is, this wouldn't do anything. ```ut_assert``` is where we start to get some of the power! This
is how we define the individual conditions that we want our code to meet. If we wanted to test
the examples given above, we would write code like this:

```c
int my_test() {
	ut_assert( square(3) == 9 );
	ut_assert( square(0) == 0 );
	ut_assert( square(1) == 1 );
	ut_assert( square(-2) == 4 );
	return 0;
}
```
Some of the other code in [Scrúdú][scrudu]'s ```main()``` would then record information about the
test and print it all out for us if we were to run the code after compiling. We can add more interesting
tests based on specific cases. For example, let's say we expanded our ```square(x)``` function to
include imaginary numbers. We could then have a test function for integers, and anothe for imaginary
numbers. Something like this:
```c
int test_integers() {
	ut_assert( square("3") == 9 );
	ut_assert( square("0") == 0 );
	return 0;
}

int test_imaginary() {
	ut_assert( square("i") == -1 );
	ut_assert( square("3i") == -9 );
	return 0;
}

int main() {
	ut_run( test_integers );
	ut_run( test_imaginary );
	return 0;
}
```
And there you have it! A simple to use unit testing framework for C.

# Memory Analysis in Scrúdú

A constant thorn in a programmer's side, at least when it comes to C, is memory management. The thing
about C (and this is what gives it a lot of its power), is that it doesn't manage the memory for you. Like,
at all. If you allocate some space for a data structure, it will stay there until you tell it to go away. 
And to make things even worse, if you lose track of where it was, say by accidentally overwriting the pointer,
it will basically be impossible to ever get that memory back – at least until the program exits. This may not
seem too bad, until you realize that this is what leads to crashes due to bad memory accesses, running out
of memory because of a so-called "memory leak", and other general frustrations that will arise. Fruthermore,
the messages you get when you crash from a memory error are often ambigious, something like "core dump", which
says absolutely nothing about the code you just wrote.

This is what inspired me to start writing a tool that would make memory debugging simpler! I wanted something
that told me exactly when memory-related crashes were occurring, possibly even why. And I wanted the
tool to tell me how much memory I was leaking, and where the code was leaking.

I should note here, before I start getting comments on this, I am entirely aware that tools to do this exact
sort sort of thing exist, like Valgrind. But I wanted something that was simple and portable, did things the
way I wanted to do them, and I also just wanted the experience of writing testing code. So if you don't like it,
that's fine. I don't care. Okay, now back to [Scrúdú][scrudu]!

The memory management tool in [Scrúdú][scrudu] works by wrapping C's native ```malloc``` and ```free``` functions
with my own code. This is done through the use of a macro, like so:

```c
#define malloc(X) memcheck_malloc( X, __FILE__, __LINE__, __FUNCTION__ )
#define free(X) memcheck_free( X )
```

This has a few neat little tricks! First, I can surround this with a ```#ifdef``` to create a variable
that turns the memory checker on or off (i.e. by passing a flag to the compiler). The other thing it lets
me do is pass more information into the allocation without having to change the source code for the 
program being built. Specifically, the macro will handle passing in extra data, such as the line number
where malloc was called, from which file it originated, and also the function that made the call. 
What this essentially means is that if the source code has something like this:
```c
int main() {
	int *x = malloc( sizeof(int) );
	free(x);
	return 0;
}
```
will become this, after the preprocessor runs:
```c
int main() {
	int *x = memcheck_malloc( sizeof(int), __FILE__, __LINE__, __FUNCTION__ );
	memcheck_free(x);
	return 0;
}
```
Then I can define the two functions above (i.e. ```memcheck_malloc()``` and ```memcheck_free()```)
somewhere in the [Scrúdú][scrudu] code, and these functions handle some processing and checks before
passing the parameter, `X`, to the actual `malloc` and `free` funtions. This functionality is in the file
memcheck.c and is defined, roughly, like this:
```c
void *memcheck_malloc( size_t size, const char *file, int line, const char *function ) {
	void *ptr = malloc(size);
	/* do some extra stuff here */
	return ptr;
}
```
And something similar for free. 

The extra processing that takes place is basically just maintaining a linked list which stores the extra
data passed to `memcheck_malloc()` and `memcheck_free()`. The allocation part will store the infromation
in a list node, and the free part will look for the address being freed in the linked list, and remove it 
before calling the actual free. What this means is that if the list is not empty by the end of the program
running, then some memory was leaked. To make things even easier to debug, the list is printed at the end of
the `main()` function in scrudu.c, so you can see exactly which function call leaked the memory (or at least
which function allocated the leaked memory). 

One thing that is worth noting here is the issue of self-referential macros. This basically just means
that the wrapper function calls `malloc` itself, which would be expanded by the preprocessor into the same
thing, making it a recursive function call. That means trying to debug the memory with these wrappers would,
somewhat ironically, cause the program to crash due to a memory error. There are a few workarounds for this,
but the one I went with was to call `#undef` in the .c file where the wrapper functions are defined. This means
that as far as that file is concerned, there are no wrapper macros.

So, how do you make use of all of this? Simple! Define your test functinos in scrudu.c, just like we did
for the unittesting part of the code, then include scrudu.h in the source files you want to test. They will
call the wrappers everywhere a call to `malloc` is made! You could even use your own source files and ignore
scrudu.c, but you will want to call the `memcheck_printtable()` function so that you can actually see where
you are getting errors, if you are getting them.

That is all for now! In future, I may expand on this post and add in a more advanced tutorial on how I built
the specific components, but this should act as a good overview! Happy coding!

[minunit]: http://www.jera.com/techinfo/jtns/jtn002.html
[unittest]: https://github.com/Gr1m3y/unittest
[scrudu]: https://github.com/Gr1m3y/Scrudu
