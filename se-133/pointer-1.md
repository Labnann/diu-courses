# Pointer
## TLDR

We declare a pointer variable by putting an asterisk at the left side of its name.

```c
int *p;
```

The pointer can keep address of some other variable.

```c
int *p;
int x = 10;
p = &x;
```

Value of p is some address of x. We can print it to find out the address if we want.
We dereference a pointer with the * operator.

So,

```c
int x = 10;
int *p = &x;
printf("%d", *p); // will print value of x ie. 10
```

And:

```c
int x = 10;
int *p = &x;
*p = 50;
```

This will change value of x to 50.

##  Explanation
Let's go back to our scan code.

```c
int x;
scanf("%d", &x);
```

What does `&x` mean here?

Address of x.

`scanf` takes the address of x so that it can put the value into it.

Pointer is a variable that stores an address.

We define a pointer and use it like this:

```c
int x;
int *p = &x;
```

Now if we want we can use the pointer instead of &x.

```c
scanf("%d", p);
```

Now, let's do some experiment with pointer to learn more about it:

```c
int x = 5;
int *p = &x;
```

What's the value of `p`?

Honestly, we don't know. It is the address chosen by the OS for x. It could look something like: 10000.

We can find it out by this line of code:

```c
printf("%d", p); //prints the address pointer p is holding 
```

What is the value of  the pointee? (IE. what is contained at memory address contained by p?)

The answer is 5. 

We can find it out by this line of code:

```c
printf("%d", *p); //prints the pointee value 
```

* is called the dereference operator. It dereferences a pointer to find out whatever it is in the address it points to.

Can you guess the value of x?

```c
int x = 10;
int *p = &x;
*p = 50;
printf("%d", x);
```

Obviously, since *p is the value of x,  *p = 50 would change the value of x to 50. So it'll print 50.
