# Exercise 2.13
__The code body of `switch` statements is formatted differently from the other
statements. Express the formatting rule used, and explain its rationale.__

The rule is that the jump labels within the switch statement are not indented.
Indenting them would mean the actual code within the switch statement would be
indented twice, wasting screen space for no benefit. It's also somewhat
analogous to the `if`-`else` chain as each `else if` or `else` statement isn't
indented further than the previous.
