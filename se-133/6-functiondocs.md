# Documenting a function with comments

We usually document a function with comments on top of its prototype declaration.

##Why there?

Prototype is the code you "share" with your teammate/ your code's user. Because it gives compiler the instruction to find and resolve the function using the linker from other places/files if it is not found where we are calling it. So, since we are sharing prototype, might as well share the "comment doc" as well because why should the user bother with the complexity of the source code?

Anyway: here is the prototype for our square function:

```c
int square (int x);
```

And before this we write the comment:
```c
/*
 * square: squares a given number
 * @param x: the number to square
 * @return the squared number
 */
int square (int x);

```
## Note that I used:

@param for parameters <br>
@return for return value

## Why this particular style?

Well these are all in `/* */` so compiler does not care about what is in there anyway. But this commenting style helps external programs like Doxygen or Javadoc (For Java) to easily create documentation for our code. Plus it is pleasing to see and easy to understand.

‎
