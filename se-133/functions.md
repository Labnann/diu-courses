# Let's talk about functions.

Consider our previous FizzBuzz program.

```c
#include <stdio.h>

int main()
{
    int in = 1;

    for(;in;) {
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

This program is hard to read or understand. Anyone who looks at the code for the first time (And perhaps you after a month or a week) will be like: there are so many lines, conditions, loops, scanning lots of things are there. What even is happening?

What if the code was something like this?

```c
#include <stdio.h>

int main()
{
    int in = 1;

    for(;in;) {
        scanf("%d", &in);
        runFizzBuzz(in);
    }

}
```

Yeah the above code does not run. But do you see how easily understandable the above code is?

Anyone new will be like: Oh it is easy, declare a variable, enter the loop, scan a number and
use the number to runFizzBuzz program. A very beautiful piece of code.

Well running that code right now will cause error because the compiler will say:
What even is "runFizzBuzz"?

So, yes we have to define the runFizzBuzz function. And here is how:

```diff
 #include <stdio.h>
 
+  void runFizzBuzz(int in)
+  {
+      if (in % 15 == 0)
+          printf("FizzBuzz\n");
+      else if (in % 3 == 0)
+          printf("Fizz\n");
+      else if (in % 5 == 0)
+          printf("Buzz\n");
+      else printf("%d", in);
+  }


 int main()
 {
     int in = 1;

     for(;in;) {
         scanf("%d", &in);
+        runFizzBuzz(in);

-        if (in % 15 == 0)
-            printf("FizzBuzz\n");
-        else if (in % 3 == 0)
-            printf("Fizz\n");
-        else if (in % 5 == 0)
-            printf("Buzz\n");
-        else printf("%d", in);
    }

}
```

Yes, basically we cut-pasted the program and wrapped it with `runFizzBuzz(){}`. Very simple.

And the resulting code is:

```c
#include <stdio.h>

void runFizzBuzz(int in)
{
        if (in % 15 == 0)
            printf("FizzBuzz\n");
        else if (in % 3 == 0)
            printf("Fizz\n");
        else if (in % 5 == 0)
            printf("Buzz\n");
        else printf("%d", in);
}


int main()
{
    int in = 1;

    for(;in;) {
        scanf("%d", &in);
        runFizzBuzz(in);
    }

}
```

Now look how easy to read this program is! The mainfunction just takes an input and runs runFizzBuzz(input) in a loop.
That's it!

Then runFizzBuzz uses its own logic to print whatever is appropriate based on the input.

The important thing here to note is that: we are software engineers and we have to work with thousands of lines of code,
if not millions. Function helps us keep our code simple, readable and easy to work with. It helps us separate our concerns.
Like in this example: main handles the input and the loop, and runFizzBuzz handles the actual fizzbuzz program.

There are many other reasons functions are important. We will discuss later.

Now that we are motivated about functions, let's see its structure:

```c
RETURN_TYPE FUNCTION_NAME(PARAMETERS)
{
    FUNCTION BODY
}
```

Function is simply a program, so it has got "input", "processing" and "output" part.

Input is what we send it to it through parameters.<br>
processing is what we keep in the body section. <br>
output is what the function returns. <br>

Think it like this: we ask a function to do something for us, it does that thing and returns
the output. Then we work with that output.

We all have worked with a square function before in our Higher Secondary level. Let's create
a c function of that.

Ie. create a function: that takes a number from us, squares it and returns it to us.

For that, let's consider these steps:

- What will it take from us? An integer. Therefore there has to be a parameter with type int. You can name it anything though!
I will use the name: x.

```c
RETURN_TYPE FUNCTION_NAME(int x)
{
    FUNCTION BODY
}
```

- And what will it return to us? Another int. So, let's make the return type int.

```c
int FUNCTION_NAME(int x)
{
    FUNCTION BODY
}
```

- We can name our function f for now. I would like to name it square later, but to resemble our higher secondary school works, lets keep the  name f for now.

```c
int f(int x)
{
    FUNCTION BODY
}
```

- We are almost done. What should be in the function body? Of course, multiplication of x by x which will be returned.

```c
int f(int x)
{
    return x*x;
}
```

Our square function is ready. From main we can call it like this.

```c
int main()
{
    int a, b, c;
    a = f(10); // Value of a will be 100.
    int x = f(20); // Value of x will be 400.

    printf("%d", f(30)); // 900 is printed
}
```

Just like we did in our higher secondary schools, we call f(something) and it works.

Let's rename our function to square because why not? It is easier to understand that way.
So, the entire program would be:

```c
#include <stdio.h>

int square(int x)
{
    return x*x;
}

//
int main()
{
    int a, b, c;
    a = square(10); // Value of a will be 100.
    int x = square(20); // Value of x will be 400.

    printf("%d", square(30)); // 900 is printed
}
```

By the way, with the print statement we tested our function. A proper way to test is to:
compare expected and actual. Let me show you how by testing the square function.

```c
#include <stdio.h>

int square(int x)
{
    return x*x;
}


int main()
{
   printf("square(10) is expected: %d, actual: %d", 100, square(100));
   
}
```

This is called "Unit Testing", where our function is a unit.

Let's write more unit tests!

```c
#include <stdio.h>

int square(int x)
{
    return x*x;
}


int main()
{
   printf("square(10) is expected: %d, actual: %d", 100, square(10));
   printf("square(-10) is expected: %d, actual: %d", 100, square(-10));
   printf("square(5) is expected: %d, actual: %d", 25, square(5));
   printf("square(-7) is expected: %d, actual: %d", 49, square(-7));
}
```

When we are done with testing, we simply forget how the function was implemented.
Because, as I said before we work with tens of thousands of lines of code and we
can't remember every little details! This is called "Abstraction".

In an actual project, maybe you will work with your friend, your friend will
create and test the function, but you don't need to know what is in there. 
(Unless you want to work with that domain too). Or maybe it is just you, who just
finished writing one unit. If that works and well tested, you can forget about
what is in there and just work with the abstraction, in this case the function
to interact with your work!

What if we defined our square function after the main function, what would happen?

```c
#include <stdio.h>

int main()
{
   printf("square(10) is expected: %d, actual: %d", 100, square(10));
   printf("square(-10) is expected: %d, actual: %d", 100, square(-10));
   printf("square(5) is expected: %d, actual: %d", 25, square(5));
   printf("square(-7) is expected: %d, actual: %d", 49, square(-7));
}

int square(int x)
{
    return x*x;
}

```

Well it would not work. The compiler, when trying to make sense of square from main
function it will say: I don't know what square is. 

Because we declared and defined the function after main().

Anyway, thats where prototype comes in.

```c
#include <stdio.h>

int square(int x);

int main()
{
   printf("square(10) is expected: %d, actual: %d", 100, square(10));
   printf("square(-10) is expected: %d, actual: %d", 100, square(-10));
   printf("square(5) is expected: %d, actual: %d", 25, square(5));
   printf("square(-7) is expected: %d, actual: %d", 49, square(-7));
}

int square(int x)
{
    return x*x;
}

```

Noticed that I just copied function header `int square(int x)`, pasted on top, and put `;` after it.

So, what does it do?
It tells the compiler "Hey! The function square exists somewhere. If it is not in this file,
it is in some other file. But it does exist."

And at the end of compilation, the compiler asks "Linker" to find the actual function and uses that.

Interesting experiment on prototype:

Let's remove `#include <stdio.h>` from our code.

```c
int main()
{
    printf("Hello world\n");
}
```

Will it compile? Well according to stdc99+ it should not. (But our compilers aren't restrictive about it, unless we explicitely tell it to be so, so it will let us go off with a warning. So, it depends on your configuration or IDE).
And we can fix the code like this:


```c
int printf(char* x, ...);

int main()
{
    printf("Hello world\n");
}
```

Wait did we just run a code successfully without stdio.h without the compiler saying a thing?
Yes. It works because the prototype is assuring the compiler that "The function definition exists somewhere so
do not worry. Just tell the linker later to find the function later in the included files.".

Included files? Well when compiling, the compiler adds standard c library and related binaries automatically.

Last topic on this module:

What does the `main` function return? Why does it return? Where does it return?

If we do not put a return statement, it returns a 0.

Otherwise it returns whatever we put after return statement.

Where does it return? It returns the number to whoever running the program.

For example when we run from codeblocks, the number is returned to codeblocks and codeblocks displays the returning number.

```
Process returned 0 (0x0)   execution time : 0.005 s
Press any key to continue.
```

What's the purpose of this number? It is to give the runner of the code to give perspective of whether this program ran properly.

For example consider this scenario:

A game Launcher, let's say Minecraft: Launches the game. 

If Minecraft works properly and exits properly, it will exit with code 0.
The launcher then checks the number. If it is indeed 0, it understands immediately that there were no issues so it shows no error message. But if Minecraft did not exit properly: the launcher may display some error message.

Different error codes have different meaning. 

You can have a glimplse of error codes in the Linux Kernel Source code here:

https://github.com/torvalds/linux/blob/master/include/uapi/asm-generic/errno.h


So, why functions?
- It makes codes easy to read and understand as I demonstrated before.
- It helps divide our program into units.
- We gotta sell/distribute our program right? Using prototypes and functions we can move parts of our
code to some other files. And we can sell or distribute that file! 

