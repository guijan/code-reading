# Exercise 2.8
__Pick some functions or methods from the book's CD-ROM or from your environment
and determine their role using the strategies we outlined. Try to minimize the
time you spend on each function or method. Order the strategies by their success
rate.__

I read the source code of the *getent* program in OpenBSD.
I place "Consult external program documentation." at the top because a program
seems like gibberish when you come in blind with next to no idea of what the
program does.
After, "Examine how the function is used." helped greatly. I looked at the
function declarations at the top and saw they were relatively many. I thought
the program wouldn't be so trivial, but then it turned out the great majority of
the functions are implementations of a generic interface applied to particular
kinds of data, and once I knew one, I knew all the others were more or less the
same thing and began seeing easy to understand patterns in each.
I suppose "Read the code in the function body" naturally comes next.

The other 2, "guess, based on the function name" and "read the comment at the
beginning of the function." don't seem all that helpful. It's hard to trust the
behavior on the function through the name alone, and C programmers rarely seem
to document return values and inputs, often choosing to very briefly say what
the function does without strictly defining its API.
