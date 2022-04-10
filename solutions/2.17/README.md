# Exercise 2.17
__Express the examples in this section using `while` instead of `for`. Which of
the two forms do you find more readable?__

It seems the original for loops were better in all cases except for the
`readdir()` one.

The examples are in [getstops.c](getstops.c), and these snippets:
```c
	cnt = 1, t = p;
	while (cnt <= cnt_orig) {
		...

		++t, ++cnt;
	}
```
```c
	while ((dp = readdir(dd)) != NULL) {
		...
	}
```
```c
	code = 255;
	while (code >= 0) {
		...
		code--;
	}
```
```c
	i = 1;
	while (i <= nargs) {
		...
		i++;
	}
```
```c
	i = 1;
	while (i < month) {
		...
		i++;
	}
```
```c
	i = 0;
	while (i <= extrknt) {
		...
		i++;
	}
```
```c
	i = 0;
	while (i < len) {
		...
		i+++;
	}
```
