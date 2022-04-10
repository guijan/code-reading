# Exercise 2.6
__Identify the header files that are needed for using the library functions
`sscanf`, `qsort`, `strchr`, `setjmp`, `adjacent-find`, `open`, `FormatMessage`,
`XtOwn- Selection`. The last three functions are operating environment-specific
and may not exist in your environment.__

sscanf: <stdio.h>
qsort: <stdlib.h>
strchr: <string.h>
setjmp: <setjmp.h>

adjacent_find: C++ function from header <algorithm>

open: POSIX function from <fcntl.h>

FormatMessage: Win32 function from <Winbase.h>

XtOwnSelection: From the X Toolkit Intrinsics, X11/Intrinsic.h

You many notice that `adjacent-find` and `XtOwn- Selection` are not spelled the
same as in the book, I believe the book text has a typing error or similar here.
