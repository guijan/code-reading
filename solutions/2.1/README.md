# Exercise 2.1
__Experiment to find out how your C, C++, and Java compilers deal with
uninitialized variables. Outline your results and propose an inspection
procedure for locating uninitialized variables.__

I wrote an intentionally buggy program for this at [hello.c](hello.c).
Clang didn't warn about that at all, even when I passed
'-Wall -Wextra -Wpedantic -std=c99' to it. Clang's `static-build` static
analyzer did, however. It seems that in my implementation the `badstr` dangling
pointer always points to null initialized memory, maybe it would be different
for a program which has had its stack grow and shrink over its runtime.

Inspecting whether a variable was initialized should be easy. One merely has to
look at where it was declared, and find the first usage. Is it a read or a
write? If it was a read, it wasn't initialized. This may get a bit complicated
when pointers are passed or returned, the most obvious solution would be to then
read the implementation of the relevant function.
