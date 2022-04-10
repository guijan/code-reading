# Exercise 2.20
__Locate expressions containing questionable assumptions about character code
values in the book's CD-ROM. Read about the Java `Character` class test and
conversion methods such as isUpper and toLowerCase or the corresponding `ctype`
family of C.__

How many of the programs in the CD-ROM ever ran on machines that aren't ASCII or
UTF-based? As far as I'm concerned, any assumptions they make are correct.
The mistake I could find is that many don't cast the character passed to the
_ctype.h_ functions to `unsigned char`.
