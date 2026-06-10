Function pointer:

Just like all the variables, functions can be stored too.

As pointers. In fact function name itself is a pointer, and

the address of operator returns the address of

the same function (ie. doesn't really have any difference)

# How to define such pointers?

Well how do we define a normal pointer?

DataType *VariableName;

For function it's similar:

ReturnType (*VariableName) (Parameter Datatype List);

For example,

```

int x = 10;

```

We create and use a pointer for x like this:

```

int *p;

p = &x;

```

Similarly, for the function:

```

int add(int x, int y)

{

    return x + y;

}

```

We create a function pointer that can point to that function like this:

```

int (*funcp) (int, int);

funcp = &add;

```

Now,

We can call the function like this:

```

funcp(10, 20);

```

This will call `add(10,20)`

# What can we do with function pointers

## Callbacks

We can pass a function inside another function.

For example, consider the following code:

```

int sedan_fare(int distance)

{

    return distance*50;

}

int bus_fare (int distance)

{

    return distance*10;

}

int fare_calculator (

    int (*handler)(int), //a function pointer that can receive the functions we wrote above

    int distance)

{

    return handler(distance);

}

int main()

{

  printf("expected: 500, actual: %d",

                fare_calculator(&sedan_fare, 10);

  printf("expected: 200, actual: %d",

                fare_calculator(&bus_fare, 20);

}

```

By the way, here we can see that in

the calculate_fare function, handler() is

behaving based on the context. Sometimes it's calling bus fare,

sometimes it's calling sedan fare. Therefore we say that handler

has multiple forms, ie. polymorphism.

### Function Pointer Inside a Struct 

Now that we can put functions inside a variable

(*inside* would be a wrong term! but you got the

idea!), means we can put it inside a struct too.

For example:

```

struct FareCalculator {

       int (*calculate)(int);

       int vat;

}

```

Note that, the function pointer we defined inside the

struct has the same syntax as everyone else!

(So it doesn't make sense to get afraid of it).

Of course we can use it like just another normal stack.


```
int main()

{

  struct FareCalculator fc;

  fc.vat = 80;

  fc.calculate = &sedan_fare;

}

```

We can definitely call this:

fc.calculate(50);

And we can also create a function like this:

```

int calculateTotalFare(struct FareCalculator *fc, int distance)

{

   int base = fc->calculate(distance);

   int total = base + (base*vat)/100;

   return total;

}

```

From main we can use it like this:

```

calculateTotalFare(fc, 50);

```

Depending on content of `fc` appropriate function will be called.

Can you do the same for Bus and CNG?

Many (Not all) people find this process of function pointer assignment, tedious. Thus object oriented programming was created.
