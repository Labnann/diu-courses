# Dynamic memory allocation

Up until now, we have only used static memory allocation. Ie. In the following code:

```c
int main()
{
 int x;
 int w, a, b, c;
 int a [50];
}
```

All the memory allocated for them is in the stack memory.

There are several benefits of using stack memory:

1. As soon as function ends, all those memories are deallocated.
2. Faster to allocate.
3. Easy to work with.

But there are some caveats.

For example:

1. Limited
2. As soon as function ends, all those memories are deallocated. Yeah this thing can be a limitation when we don't want our machine to forget some values even after exiting a function.
3. As long as we are in the function the memory usage cannot be decreased.
4. Hard to manage.

Hence there is another type of memory location called heap. We basically ask the OS: "Hey give us memory of size x" using the stdlib's malloc function.

malloc returns a pointer to the memory region OS allocated for us.

```c

int a[50]; // A 50 int sized array, statically allocated

int *m = malloc( 50 * sizeof(int) ); // A 50 sized array, dynamically allocated

```

After we are done with the memory, we free that memory.

```c

free(m);

```

Not freeing it when we are done using it will cause memory leak. In that case, whenever the allocation code is run, the memory will be allocated and as we are not freeing it, the program will keep taking up space our main memory.

Final notes on this:

Sometimes the OS fails to allocate memory. For example if we have 8GB free memory in our system and we asked for an absurd 10GB memory, it'll definitely fail.

In that case malloc returns a NULL (ie. 0). Therefore the best practice is to always check whether memory allocation failed after malloc.

```c

int *a = malloc( 1000* sizeof(int));

 if (a == NULL) {
   // handle program accordingly 
 }

 // rest of the code

```
