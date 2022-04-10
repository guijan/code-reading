# Exercise 2.22
__Find, simplify, and reason about five nontrivial Boolean expressions in the
source code base. Do not spend time on understanding what the expression
elements mean; concentrate on the conditions that will make the expression
become true or false. Where possible, identify and use the properties of
short-circuit evaluation.__

1. From netbsdsrc/usr.bin/fmt/fmt.c:
```c
	/*
	 * The following horrible expression attempts to avoid linebreaks
	 * when the indent changes due to a paragraph.
	 */
	if (np != pfx && (np > pfx || abs(pfx-np) > 8))
		oflush();
```

Could be simplified to:
```c
	if (np > pfx || abs(pfx-np) > 8)
		oflush();
```

`np` is always `!= pfx` if it's greater than it.

2.
