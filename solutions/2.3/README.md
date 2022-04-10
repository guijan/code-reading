# Exercise 2.3
__Discuss the advantages and disadvantages of defining a macro like `STREQ`.
Consider how the C compiler could optimize `strcmp` calls.__

I can't help but see STREQ as a micro-optimization. The simplest correct
solution should be used at first, I would not use this macro.
If string comparison is a bottleneck in your program, you should probably look
into things like binary search and hash tables instead.

Compilers can inline `strcmp()`. I don't know if GCC does these days, but then
again, I just try to write the correct code first and see what happens later.
Keep in mind writing the correct code doesn't mean using blatantly incorrect
algorithms like linear search, however.
