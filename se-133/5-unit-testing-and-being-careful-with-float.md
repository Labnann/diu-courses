# Unit Testing

The process of testing smallest functional piece of a code in isolation.

## Example 
Let's say you asked your teammate to handle Fahrenheit to Celsius calculation. So, ideally, your teammate will define the function independent of you and test it, then give it to you. (Yup, one of the benefits of function is the ability to work with it independently).
‎
```c
float ctof(float c)
{
  return c*1.8+32;
}
```
‎
So, how will your teammate will test this function? 
‎
To answer this: let's consider: how do we usually test something in real life?
‎
We test it by running it and checking whether it meets our expectation. For example: to check whether the AC works, we turn on the AC and try to feel the cool air blowing.
‎
There two things here:
- Expectation: Cool air will blow
- Actual: Try turning on the AC, does cool air actually blow?
‎
Similarly, to test out function, we will simply check whether expectation and actual values are equal.
‎
‎
```c
int main()
{
  printf("ctof(0) expexted: %f, actual: %f\n", 32.0, ctof(0));
}
```
‎
We can add more Test cases if we want.
‎
‎
‎
```c
int main()
{
  printf("ctof(0) expexted: %f, actual: %f\n", 32.0 , ctof(0));
  printf("ctof(-40) expexted: %f, actual: %f\n", -40.0 , ctof(-40));
}
```
‎
After unit testing, we are sure that this part of code (ctof) works and we can ready to use it without worrying about what's in it.

## Note:
### Note 1
For now we are eye-testing whether the actual and expected values match. But we can definitely automate that as well.

Just by doing something like:

```c
int main()
{
   printf("ctof(0) expexted: %f, actual: %f, success: %d\n", 32.0 , ctof(0), 32.0 == ctof(0));
}
```
The main point is observing whether actual and expected values match.

### Note 2
Always handle floating numbers in C with care. For example:
```
float x = 5/3;
``` 
here X will be 0 since C will process it like:
"5 is an int. And 3 is int. So 5/3 is 0" which is wrong.

Also floating point number has precision issues and even how I
compared it above is not the proper way.

### Note 3
Even the comparison up there, ie ` 0 == ctof(0) ` has issues.
Floating point calculation on machines don't tend to be accurate
to the last digit and comparisons too need to be handled with care.

## Full code for this lesson
```c
#include <stdio.h>

float ctof(float c)
{
  return c*1.8+32;
}

int main()
{
  printf("ctof(0) expexted: %f, actual: %f\n", 32.0 , ctof(0));
  printf("ctof(-40) expexted: %f, actual: %f\n", -40.0 , ctof(-40));
  /// Without eye-testing
   printf("ctof(0) expexted: %f, actual: %f, success: %d\n", 32.0 , ctof(0), 32.0 == ctof(0));
}
```
