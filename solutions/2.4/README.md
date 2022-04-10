# Exercise 2.4
**Look in your environment or on the book's CD-ROM for programs that do not
verify the result of library calls. Propose practical fixes.**

In *sourcecode/netbsdsrc/sbin/ifconfig/ifconfig.c* I see a `strncpy()` that does
not check its return value right after the `getopt()` loop in `main()`.
It copies to an array of 30 char straight from user input, you can make it put
an invalid string into its destination by passing a 30 character long interface
name.
The bug fix is to simply turn the array the `strncpy()` call copies to into a
pointer and assign the pointer to the string to it, the copying the string is
not necessary in the first place.

There are many other uses of `strncpy()` in that source file, I haven't checked
them, but the usual fix is to use the extension `strlcpy()` instead. One should
not worry about the portability of this extension, first because NetBSD only
builds on NetBSD anyway, but also because it can be trivially implemented in
Standard C. It didn't exist when that source code was written though.
