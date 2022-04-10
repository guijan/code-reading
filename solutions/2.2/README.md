# Exercise 2.2
__(Suggested by Dave Thomas.) Why can't the *echo* program use the `getopt`
function?__

It actually can, only the code would be very ugly. It's easy to break out of
the typical "`getopt()` loop" construct if the -n flag is repeated, and it's
possible to disable diagnostic messages by setting `opterr` to `0` and making
the first character of `optstring` a `':'`. this is way more complicated than
simply not using `getopt()` though.
