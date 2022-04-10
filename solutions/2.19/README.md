# Exercise 2.19
__Locate ten occurrences of `break` and `continue` in the source code provided
with the book. For each case indicate the point where execution will transfer
after the corresponding statement is executed, and explain why the statement is
used. Do not try to understand in full the logic of the code; simply provide an
explanation based on the statement's use pattern.__

1. OpenBSD /usr/src/bin/ed/io.c
```c
/* get_extended_line: get a an extended line from stdin */
char *
get_extended_line(int *sizep, int nonl)
{
	static char *cvbuf = NULL;		/* buffer */
	static int cvbufsz = 0;			/* buffer size */

	int l, n;
	char *t = ibufp;

	while (*t++ != '\n')
		;
	if ((l = t - ibufp) < 2 || !has_trailing_escape(ibufp, ibufp + l - 1)) {
		*sizep = l;
		return ibufp;
	}
	*sizep = -1;
	REALLOC(cvbuf, cvbufsz, l, NULL);
	memcpy(cvbuf, ibufp, l);
	*(cvbuf + --l - 1) = '\n'; 	/* strip trailing esc */
	if (nonl)
		l--; 			/* strip newline */
	for (;;) {
		if ((n = get_tty_line()) < 0)
			return NULL;
		else if (n == 0 || ibuf[n - 1] != '\n') {
			seterrmsg("unexpected end-of-file");
			return NULL;
		}
		REALLOC(cvbuf, cvbufsz, l + n, NULL);
		memcpy(cvbuf + l, ibuf, n);
		l += n;
		if (n < 2 || !has_trailing_escape(cvbuf, cvbuf + l - 1))
			break;
		*(cvbuf + --l - 1) = '\n'; 	/* strip trailing esc */
		if (nonl) l--; 			/* strip newline */
	}
	REALLOC(cvbuf, cvbufsz, l + 1, NULL);
	cvbuf[l] = '\0';
	*sizep = l;
	return cvbuf;
}
```
Execution will continue 3 lines below, the statement is used because either n is
1 (which means the only character in the line is the newline as guaranteed by
the preceding code), or the newline is not escaped, which means the function has
fetched the line it needed.

2. OpenBSD /usr/src/bin/ed/main.c:
```c
	while ((c = getopt(argc, argv, "p:sx")) != -1)
		switch (c) {
		case 'p':				/* set prompt */
			dps = prompt = optarg;
			break;
		case 's':				/* run script */
			scripted = 1;
			break;
		case 'x':				/* use crypt */
			fprintf(stderr, "crypt unavailable\n?\n");
			break;
		default:
			fprintf(stderr, usage, argv[0]);
			exit(1);
		}
```
In each case, the execution continues after the switch statement, in this case
it's inside a while loop and the switch is the only statement in the loop, so it
ocntinues in the while loop's condition. This is the typical `getopt`() loop.

3. OpenBSD /usr/src/bin/ed/main.c:
```c
static int
get_shell_command(void)
{
	static char *buf = NULL;
	static int n = 0;

	char *s;			/* substitution char pointer */
	int i = 0;
	int j = 0;

	if ((s = ibufp = get_extended_line(&j, 1)) == NULL)
		return ERR;
	REALLOC(buf, n, j + 1, ERR);
	buf[i++] = '!';			/* prefix command w/ bang */
	while (*ibufp != '\n')
		switch (*ibufp) {
		default:
			REALLOC(buf, n, i + 2, ERR);
			buf[i++] = *ibufp;
			if (*ibufp++ == '\\')
				buf[i++] = *ibufp++;
			break;
		case '!':
			if (s != ibufp) {
				REALLOC(buf, n, i + 1, ERR);
				buf[i++] = *ibufp++;
			}
			else if (shcmd == NULL)
			{
				seterrmsg("no previous command");
				return ERR;
			} else {
				REALLOC(buf, n, i + shcmdi, ERR);
				for (s = shcmd + 1; s < shcmd + shcmdi;)
					buf[i++] = *s++;
				s = ibufp++;
			}
			break;
		case '%':
			if (*old_filename  == '\0') {
				seterrmsg("no current filename");
				return ERR;
			}
			j = strlen(s = strip_escapes(old_filename));
			REALLOC(buf, n, i + j, ERR);
			while (j--)
				buf[i++] = *s++;
			s = ibufp++;
			break;
		}
	if (i == 1) {
		seterrmsg("no command");
		return ERR;
	}
	REALLOC(shcmd, shcmdsz, i + 1, ERR);
	memcpy(shcmd, buf, i);
	shcmd[shcmdi = i] = '\0';
	return *s == '!' || *s == '%';
}
```
This is the same kind of code as the 2nd case, only it`s parsing an input line,
a command to the ed text editor.

4. OpenBSD /usr/src/lib/libc/hash:
```c
char *
HASHFileChunk(const char *filename, char *buf, off_t off, off_t len)
{
	struct stat sb;
	u_char buffer[BUFSIZ];
	HASH_CTX ctx;
	int fd, save_errno;
	ssize_t nr;

	HASHInit(&ctx);

	if ((fd = open(filename, O_RDONLY)) == -1)
		return (NULL);
	if (len == 0) {
		if (fstat(fd, &sb) == -1) {
			save_errno = errno;
			close(fd);
			errno = save_errno;
			return (NULL);
		}
		len = sb.st_size;
	}
	if (off > 0 && lseek(fd, off, SEEK_SET) == -1) {
		save_errno = errno;
		close(fd);
		errno = save_errno;
		return (NULL);
	}

	while ((nr = read(fd, buffer, MINIMUM(sizeof(buffer), len))) > 0) {
		HASHUpdate(&ctx, buffer, nr);
		if (len > 0 && (len -= nr) == 0)
			break;
	}

	save_errno = errno;
	close(fd);
	errno = save_errno;
	return (nr == -1 ? NULL : HASHEnd(&ctx, buf));
}
```

It's a very simple case. This is a `read()` loop that handles partial writes.
The break statement obviously exits the loop, the "len > 0" bit is redundant.
It hashes a cunk of a file, as the function's aptly named identifier suggests.
of code is redundant.

5.
