# Exercise 2.18
__Devise a style guideline for specifying when `while` loops should be used in
preference to `for` loops. Verify the guideline against representative examples
from the book's CD-ROM.__

1. Where the initialization and the increment are the same, use a while loop.

For code like:
```c
	for (dir = readdir(dirp); dir != NULL; dir = readdir(dirp))
```
Write this instead:
```c
	while ((dir = readdir(dirp)) != NULL)
```

I've skimmed the XFree86 and NetBSD source from the CD-ROM, as well as the
latest copy of the OpenBSD source tree, and I didn't find any source code I'd
change.
