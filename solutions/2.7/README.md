## Exercise 2.7
__Examine the visibility of functions and variables in programs in your
environment. Can it be improved (made more conservative)?__

Recently I did just that to a program called *scrot*.

Browsing OpenBSD source code, I see its implementation of *expand* suffers from
the same issue: `nstops` and `tabstops` could be made static.
I went ahead and looked at the related *unexpand* program, and not only can 2
global variables be made static, but also there's a whole function called
`tabify` which could be static.
I then decided to look at a random program with a name that sounded interesting,
I ended up in a program called *fsirand*, and the variables `printonly`,
`force`, and `ignorelabel` could be made static, as well as the functions
`usage()` and `fsirand()`.
All of these were single source file programs, so I decided to try a file with
multiple source files, and lo and behold `ctags` is a program composed of
multiple *.c* files and contains the functions `init()`, `find_entries()`, and
`preload_entries()`, all of which could be made static. Also, the objects
pointed to by `find_entries()`' and `preload_entries()`' pointer parameters
could be made const.
