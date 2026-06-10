# Condition and Loop

## Consider the following problem:

Take a number input from the user.
If the number is divisible by 3, print "Fizz".
If the number is divisible by 5, print "Buzz".
If divisible by both, print "FizzBuzz".
Otherwise, just print the number.

## The solution of the problem would be:


```c
#include <stdio.h>

int main()
{
    int in;

    scanf("%d", &in);

    if (in % 15 == 0)
        printf("FizzBuzz\n");
    else if (in % 3 == 0)
        printf("Fizz\n");
    else if (in % 5 == 0)
        printf("Buzz\n");
    else printf("%d", in);
}
```

## Let's talk about control statements
### such as if, if ... else, for, while etc.

From ISO-C specification, `if` is one of the `selection statements`.
Syntax:

`if (expression) secondary-block`
`if (expression) secondary-block else secondary-block`

if the expression results in anything other than 0, it is considered true.<br>
if the expression results in 0, it is considered false.<br>

if true, the immediate secondary block will be executed.<br>
if false, the secondary block in the `else` section will be executed if it exists.

Now, the customer of our FizzBuzz program wants change. The customer
says, "I don't want to run this program again and again. Can you accomodate
that?".

Yeah, as Software Engineers we have to deal with changes again and again,
in many ways. Only a software that nobody uses does not change. We call
that a dead software.

Anyway, how do we accomodate that? Well, put the part we want to repeat
again and again in a loop. Let's use a while loop to do it!


```c
#include <stdio.h>

int main()
{
    int in;

    while(1) {
        scanf("%d", &in);

        if (in % 15 == 0)
            printf("FizzBuzz\n");
        else if (in % 3 == 0)
            printf("Fizz\n");
        else if (in % 5 == 0)
            printf("Buzz\n");
        else printf("%d", in);
    }

}
```

Note that we just wrapped with `while(1){<Previous Code Here>}`

Now, run the code. It keeps repeating the input and output process!

The syntax for while is basically the same as `if`.

`while(expression) secondary-block`

The secondary block will keep running as long as the expression is true.
(Note: we discussed above what is considered true.)

Now, can you guess the behavior of this code? I have showed the changes I made
in the code through comments.

```c
#include <stdio.h>

int main()
{
    int in = 1; // This line is changed

    while(in) { // This line is changed 1 -> in
        scanf("%d", &in);

        if (in % 15 == 0)
            printf("FizzBuzz\n");
        else if (in % 3 == 0)
            printf("Fizz\n");
        else if (in % 5 == 0)
            printf("Buzz\n");
        else printf("%d", in);
    }

}
```

Yes, the behavior will stay the same, except if we input 0, the loop will break.

Why will this loop break? Because the expression, which is our `in` variable
contains our input. If we scan 0 into it, the next time, the `while(in)` will
be evaluated into `while(0)` and will end up breaking it.


Now, let us talk about for loop. The equivalent of previous program in for would be just changing
`while(in)` with `for(;in;)`:


```c
#include <stdio.h>

int main()
{
    int in = 1; 

    for(;in;) { // This line is changed
        scanf("%d", &in);

        if (in % 15 == 0)
            printf("FizzBuzz\n");
        else if (in % 3 == 0)
            printf("Fizz\n");
        else if (in % 5 == 0)
            printf("Buzz\n");
        else printf("%d", in);
    }

}
```

What does that tell us about for loop?

The for statement
`for (clause-1; expression-2; expression-3)`

behaves as follows:

The expression `expression-2` is the controlling expression that is evaluated `before`
each execution of the loop body.

The expression `expression-3` is evaluated as a void expression `after` each execution
of the loop body.

If `clause-1` is an expression, it is evaluated as a void expression `before` the first 
evaluation of the controlling expression. If it is a declaration, the scope of anything
it declares is upto the end of the loop.

Clause-1 and Expression-3 can be empty.
Expression-2 can be empty, but it will be evaluated to true. (Ie. don't break the loop here.)

Mainly, we use for loop for:
Clause-1 for Declaration/initialization. <br>
Expression-2 for Controlling whether the loop should break. <br>
Expression-3 for increament or decreament.


The `do ... while` loop is similar to while loop, except the loop body part executes at least once.
Well it makes sence because the condition checking is postponed, right?

```c
#include <stdio.h>

int main()
{
    int in = 1; 
    int a, b;

    do { // This line is changed
        scanf("%d", &in);

        if (in % 15 == 0)
            printf("FizzBuzz\n");
        else if (in % 3 == 0)
            printf("Fizz\n");
        else if (in % 5 == 0)
            printf("Buzz\n");
        else printf("%d", in);
    } while(in); // This line is changed

}
```


Some simple experiments with for loop:

Can you guess how many times this program will ask for input?

```c
#include <stdio.h>

int main()
{
    int in = 1; 
    int a, b;

    for(int i =0; i<10; i++) {
        scanf("%d", &in);

        if (in % 15 == 0)
            printf("FizzBuzz\n");
        else if (in % 3 == 0)
            printf("Fizz\n");
        else if (in % 5 == 0)
            printf("Buzz\n");
        else printf("%d", in);
    }

}

```

10 times. Because i starts with 0, after each loop it is increased by 1
and when i is 10, the i<10 fails, ending the loop.


Can you guess output of this one?

```c
#include <stdio.h>

int main()
{
    int in = 1;
    int a, b;

    int i, j, k;

    for(i=0, j=1, k=2; j<10; i++, k++) { 
        scanf("%d", &in);

        if (in % 15 == 0)
            printf("FizzBuzz\n");
        else if (in % 3 == 0)
            printf("Fizz\n");
        else if (in % 5 == 0)
            printf("Buzz\n");
        else printf("%d", in);
    }

}
```

Well this loop is infinite because the condition j<10 will never break because j is always 1 and
nothing is changing it.

Break and continue statements:<br>
A break statement causes the loop to break immediately.<br>
A continue statement causes the loop to not proceed farther and resume the next iteration.<br>


break: example:

Consider the following c code:

```c
#include <stdio.h>

int main()
{
    int in = 1;
    int a, b;

    int i, j, k;

    for(i=0, j=1, k=2; j<10; i++, k++) { 
        scanf("%d", &in);

        if (in % 15 == 0) {
            printf("FizzBuzz\n");
            break;
        }
        else if (in % 3 == 0)
            printf("Fizz\n");
        else if (in % 5 == 0)
            printf("Buzz\n");
        else printf("%d", in);
    }
    printf("Done\n");

}
```

In this case: after printing FizzBuzz no input will be taken, the program will print Done and exit.


```c
#include <stdio.h>

int main()
{
    int in = 1;
    int a, b;

    int i, j, k;

    for(i=0, j=1, k=2; j<10; i++, k++) { 
        scanf("%d", &in);

        if (in % 15 == 0) {
            printf("FizzBuzz\n");
            continue;
        }
        else if (in % 3 == 0)
            printf("Fizz\n");
        else if (in % 5 == 0)
            printf("Buzz\n");
        else printf("%d", in);

        printf("Done looping\n");
    }
    printf("Done\n");

}
```

In this example, everytime Fizz or Buzz is printed, "Done looping" is printed too. However in
case of "FizzBuzz", after Fizz or Buzz is printed the program flow goes back to begining of loop hence Done Printing is not printed.
