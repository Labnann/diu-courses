# Pointer arithmetic 

Consider the given code:

```c
int x;
int *p = &x;
```

What is the value of p? It is the address of x.

We can find it out by printing: p or &x.

```c
printf("%u\n", p);

```

(Why are we using %u? So that we get a positive number)

Let's say we got: 100500

Observe: what will be  p+1?

100504

What will be  p+2?

100508

What will be  p+3?

100512

Do you see a parrern? It is increasing by 4 for each increment. Why 4?

Because it is an integer pointer and  4 is the size of integer. When we add 1 to the pointer, it points to the next integer which is 4 bytes away.

## Relation to our array lesson:

Assume an array:

```c

int a = {7, 21, 5, 10, 20};

```

We understand that a[0] is 7, a[1] is 21 etc but what is `a`?

It is actually a pointer to a[0].

Now, observe the following code and its behavior:

```c
printf("%d\n", *a); // prints 7

printf("%d\n", *(a+1)); // prints 21

printf("%d\n", *(a+2)); // prints 5
```

By the way: it is obvious but be aware of the fact that:

```c
printf("%d\n", *a+1); // prints 8
```

printd 8 because \*a is 7 and \*a + 1 is 8.
