# Exercise 2.16
__The `for` statement in the C language family is very flexible. Examine the
source code provided to create a list of ten different uses.__

1. Iterate over a buffer, until a sentinel value is found.
```c
	for (; *argv; argv++) {
		...
	}
```

2. The classic `for` loop, run a loop a specific number of times.
```c
	for (i = 0; i < mntsize; i++) {
		...
	}
```

3. Count the amount of something.
```c
	/* Count the number of types. */
	for (i = 1, nextcp = fslist;
	    (nextcp = strchr(nextcp, ',')) != NULL; i++)
		++nextcp;
```

4. The inverse of the classic for loop: run something a specific number of
   times, while counting down.
```c
	for (p = b; length--;)
			*p++ = '\0';
```

5. Loop infinitely.
```c
	for (;;) {
		...
	}
```

6. Loop with a complex condition
```c
	for (;;) {
		if (isdigit(c)) {
			val = (val * base) + (c - '0');
			c = *++src;
		} else if (base == 16 && isxdigit(toupper(c))) {
			val = (val << 4) |
				(toupper(c) + 10 - 'A');
			c = *++src;
		} else
		break;
	}
```

7. Loop with a condition that does not go at the top or the bottom.
```c
	for (;;) {
		...
		if (...)
			break;
		...
	}
```

8. Traverse a list.
```c
	for (pp = proclist.p_next; pp; pp = pp->p_next) {
		...
	}
```

I've spent an hour or 2 skimming source code, I only really got 8 distinct uses.
