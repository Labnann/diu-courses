# Refactoring

Changing the internal structure of the code without changing the external behavior or functionality.

## Question: Can you fix a bug while refactoring?

No, you can't. Because fixing a bug means altering the behavior of our porgram. Which, by definition
would not be refactoring.


# Examples of refactoring:

Consider the following program:

```c
#include <stdio.h>

int main()
{
  int x;
  scanf("%d", &x);
  
  if (x < 0)
    printf("Absolute value of %d is %d ", x, -x);
  else
    printf("Absolute value of %d is %d ", x, x);
}
```

We can refactor and rename the variable x to input.

```c
#include <stdio.h>

int main()
{
  int input;
  scanf("%d", &input);
  
  if (input < 0)
    printf("Absolute value of %d is %d ", input, -input);
  else
    printf("Absolute value of %d is %d ", input, input);
}
```

We have successfully refactored and renamed the variable.

We can refactor farther if we want.

Notice that the print statements look very similar, with only one difference.
So, let's do something like this:

```c
#include <stdio.h>

int main()
{
  int input;
  scanf("%d", &input);

  if (input < 0)
    input = -input;

  if (input < 0)
    printf("Absolute value of %d is %d ", input, input);
  else
    printf("Absolute value of %d is %d ", input, input);
}
```

Now the if condition that prints is not even necessary anymore. Because both branches do the same thing! So, let's get rid of it.

```c
#include <stdio.h>

int main()
{
  int input;
  scanf("%d", &input);

  if (input < 0)
    input = -input;

  printf("Absolute value of %d is %d ", input, input);
}
```

We can refactor farther!

Let's move the absolute value calculation logic to a function.

```c
#include <stdio.h>

int absoluteValue(int input)
{
  if (input < 0)
    input = -input;
    
  return input;
}

int main()
{
  int input;
  scanf("%d", &input);

  printf("Absolute value of %d is %d ", input, absoluteValue(input));
}
```

Notice that how readable and understandable the code is right now!

The line:
```c
printf("Absolute value of %d is %d ", input, absoluteValue(input));
```
basically self explains what it is doing.

This way, we refactor a code to gradually make it better and better.

What part of the code do you want to improve next?




