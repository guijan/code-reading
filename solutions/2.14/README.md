# Exercise 2.14
__Examine the handling of unexpected values in `switch` statements in the
programs you read. Propose changes to detect errors. Discuss how these changes
will affect the robustness of programs in a production environment.__

A skim through some source trees showed me programs that either correctly
handled unexpected values, or assumed the value was within a certain collection
of values, and this value was completely under the program's control.
