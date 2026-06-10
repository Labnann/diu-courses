# Ternary and boolean operators

## Let's start with a simple program:

Write an absolute value function and test it.

```c
#include <stdio.h>

int abs(int x)
{
    if (x < 0 )
        return -x;
    
    return x;
}


int main()
{
    printf("abs(-6), expected: %d, actual: %d" 6, abs(-6));
    printf("abs(10), expected: %d, actual: %d" 10, abs(10));
}
```

Here we used  the < operator right?

that's a boolean operator. There are other boolean operators like:

```
>, == , != , && , || , >=, <= 
```

I won't be going in depth about them. Just know that they evaluate to 0 or 1 where 1 means  true
and 0 means false. Just some examples for you to guess the output:

```
x = 10 > 5
```
What is the value of x? 1


```
int x = 10;
int y = 5;

int z = x == y;
```
What is the value of z? 0. Because x is not equal to y.

Some more examples:

```c
int x = 10;
int y = 5;

int a = x || y; // a is 1
int b = x > y; // b is 1
int c = a && b; // c is 1
int d = x < y; // d is 0
int e = (x > y)  + 100; // e is 101
int f = (x > y)  + (a  != b); // f is 1
int g = (x > y)  + (x != b); // g is 2
int h = (x > y)  || (x == b); // g is 1
```

## Ternary operator "?":

This is another control operator.

Evaluates the condition, then if true: executes the first, otherwise executes the second part.

So:

```c
x = 10 > 5? 50: 100;
// 10 > 5 is true so x will actually turn into 50 because 50 is the first one.

x = 10 < 5 ? 50: 100;
// 10 < 5 is false. So x will turn into 100 because  the second part is 100.

return 10 < 5 ? 50: 100;
// it will return 100 because 10 < 5 is false so the second part will be taken. 
```



Can you guess what the value of z is?

```c
int x = 10; 
int y = 15;
int a = 40;
int b = -30;

int z = x > y? a:b;
```

Anothe rimplementation of our absolute value function:


```c

int abs(int x)
{
    return x < 0? -x: x;
}
```

It checks the parameter x whether it is less than 0. If it is less than 0
-x is selected for returning. Otherwise x is selected for returning.

In fact this is how it is in the standard C library for stdlib.h!

https://github.com/bminor/glibc/blob/master/stdlib/abs.c

```c
/* Copyright (C) 1991-2024 Free Software Foundation, Inc.
   This file is part of the GNU C Library.
   The GNU C Library is free software; you can redistribute it and/or
   modify it under the terms of the GNU Lesser General Public
   License as published by the Free Software Foundation; either
   version 2.1 of the License, or (at your option) any later version.
   The GNU C Library is distributed in the hope that it will be useful,
   but WITHOUT ANY WARRANTY; without even the implied warranty of
   MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU
   Lesser General Public License for more details.
   You should have received a copy of the GNU Lesser General Public
   License along with the GNU C Library; if not, see
   <https://www.gnu.org/licenses/>.  */
#include <stdlib.h>
#undef	abs
/* Return the absolute value of I.  */
int
abs (int i)
{
  return i < 0 ? -i : i;
}
```

