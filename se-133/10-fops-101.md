# File operation basics
### For easier understanding, do  everything described here in a newly created folder/ directory 

stdio.h needs to be included for the following two sections.

## File writing basics

Remember how to use printf?

Of course. Let's write our hello world program! 

And... let's also print a variable.

```c
int main()
{

    int x = 10;
    printf("Hello world: %d", x);
}

```

This prints hello world on the screen.

Now this can be rewritten like this:

```c
int main()
{
    int x = 10;
    fprintf(stdout, "Hello world: %d", x);
}
```

Let's run it. This works too!
Okay so what is happening here?

Actually stdout is the "File" that is connected to our console which shows our outputs.

That's why it works!

What if we want to print to some other file?
We open the file in write mode, instead of stdout we use the file, print into it and save it. Done.

```c
int main()
{

    FILE fp = fopen("hello.txt",  "w");
    int x = 10;
    fprintf(fp, "Hello world: %d", x);
}

```

Now compile and run the program. There should be a hello.txt file in our working folder/directory. 

By the way, the first parameter of fopen is path/to/where/my/file/is/thefile

ie. it says where the file exists or where it should be created in case of write mode.

And of course, it  will contain:

```

Hello world 10

```

## File reading basics

File reading, ie. input from a file.

Remember how we take user input from console?

Using scanf.

Now like before we'll use fscanf to scan from our console.

A file named stdin is connected to the console for this. Basically, if we unbox scanf we will find fscanf happening on the stdin file. Whatever is written by user on the console is forwarded to stdin.

Therefore,

```c
int main()
{
   int x;
   scanf("%d", &x);
   printf("scanned: %d", x);
}

```

can be rewritten like this:

```c

int main()
{
   int x;
   fscanf(stdin, "%d", &x);
   printf("scanned: %d", x);
}

```

Now that we have unboxed scanf to get fscanf and demonstrated how it works the same with stdin, we can use a file here instead to get inputs from there!

Now let's do our experiment.

Let's create a file named `scanme.txt` in our folder using any text editor.

(Understand that a file name doesn't have to end with .txt)

Let's put the following numbers in them:

```
1 22 333 4444 55555
```

Now let's rewrite our code:

```c
int main()
{
   FILE *fp = fopen("scanme.txt", "r");
   int x;
   fscanf(fp, "%d", &x);
   printf("scanned: %d", x);
}
```

Now, of course, running this code will result in printing:

```
scanned: 1

```

in the console. Why only 1 is scanned? Because scanf %d is supposed to scan only one decimal. Nothing different from the ordinary.

By the way, notice that "r" in fopen. It means we are telling the operating system to open the file in read mode.

Now let's scan all the numbers and sum them all.

```c
int main()
{
   FILE *fp = fopen("scanme.txt", "r");
   int x;
   while(1)
   {
      fscanf(stdin, "%d", &x);
      printf("scanned: %d", x);
   }
}
```

Well, this code now will indefinitely keep scanning and printing whatever it inputs. As it is an infinite loop.

Well we can't run this loop forever! We have other tasks to do. What about summing the numbers? Therefore we gotta stop at some point!

scanf , fscanf, sscanf and other related scan functions return a value: "How many scans were done successfully". 

If it fails to scan something or hits end of file, it returns EOF (typically #define ed with -1). The name EOF came from End of File.

Therefore we can check the return value of the scan function for EOF, to determine when we don't need to scan anymore.
Let's modify our code based on what we discussed above:

```
int main()
{
   FILE *fp = fopen("scanme.txt", "r");
   int x;

   while(1)
   {
      int r = fscanf(stdin, "%d", &x);

      if ( r == EOF)
         break;

      printf("scanned: %d", x);

   }

}
```

Awesome! We can now scan those numbers from the file, and we also can determine when we have reached the end of file.

Now let's sum those numbers and be done with it.

```
int main()
{
   FILE *fp = fopen("scanme.txt", "r");

   int x;
   int sum = 0;

   while(1)
   {
      int r = fscanf(stdin, "%d", &x);
      if ( r == EOF)

         break;

      sum = sum + x;

   }

   printf("sum: %d", sum);
}
```



## Error handling 

In the codes we written above, for simplicity we skipped error handling. Let's learn that now.

We are asking the OS through fopen to open a file for reading, writing, appending etc. That doesn't mean OS will always be able to open the file for us!

- The file we want to read may not exist!

- The file we want to create may not be created due to lack of Disk Space! Or simply that the path mentioned there doesn't exist.

If the Operating System fails to open for us the file we want, it doesn't make sense to read that file, or write that file. Therefore, such issue need to be handled.

Basically, when `fopen` fails to open file, it returns a 0 or NULL, we can just check for it to avoid invalid file processing activities.

```

FILE *fp = fopen("scanme.txt" , "r");

if (fp == NULL) {
   printf ("File couldn't be opened!");
   return -1;
}

```

## Position at file stream

### ftell

A file is a read/written as stream. It's like reading a book, going page by page, or watching a video. Not everything at once, rather bit by bit, sequentially we access it. Why? Because as a human, we can't read a whole book at one sight, or watch an hour of video in a momen. Similarly files can be large. And it is safer to access bit by bit sequentially instead of loading whole thing at once (or mapping it with main memory) because we may not even have enough memory fot that. This also gives us control over what is being loaded in the memory.

Enough theories. 

The purpose of ftell is to tell which position of file we are currently at.

To understand this, let's modify our above program:



```
int main()
{
   FILE *fp = fopen("scanme.txt", "r");
   int x;
   int sum = 0;

   while(1)
   {
      int pos = ftell(fp);
      printf("%d " , pos);
      int r = fscanf(stdin, "%d", &x);
      if ( r == EOF)
         break;

      sum = sum + x;

   }

   printf("sum: %d", sum);
}

```

Let's run it. What's the output?

```
0 1 4 8 13 19
sum: 60355
```

Lets use a table to understand the output:

Our input from scanme.txt was:
```
1 22 333 4444 55555
```

Now, before scanning we were at position 0, so output was 0.

After scanning we consumed one decimal input "1", hence the position moved 1 character length right, hence it outputs 1.

At next scan we get 22. This skipped over one space and scanned two digits. So our next position is: previous (1) + 3  = 4.

Can you explain why rest of the output is 8 13 19?

### fseek

So far we have seen that we can only move forward with our file stream. How would we move back?

That's where fseek comes to play.

With this we can move to any position of a file stream, or skip a bit. Let's see how it works.

`fseek(file pointer, offset, from where?)`

file pointer would be fp, offset is just a number saying how far.

Let's use it!



```c

int main()

{

   FILE *fp = fopen("scanme.txt", "r");
   int x;
   int sum = 0;

   while(1)
   {
      int pos = ftell(fp);
      printf("%d " , pos);
      int r = fscanf(stdin, "%d", &x);

      if ( r == EOF)
         break;

      sum = sum + x;
   }

   printf("\nsum: %d\n", sum);
   fseek(fp, 4, SEEK_SET);

   fscanf(stdin, "%d", &x); 
   printf("scanned: %d\n", x);

}

```

We used fseek to seek to position 4 from SEEK_SET. SEEK_SET basically means from the beginning, so after fseek fp will be at position 4.

Therefore scanning for an integer, we will receive 333 since the next number at position 4 is 333.

## The manpages

How do we remember SEEK_SET, or fopen, or fclose or anything related to that?

Well, use manpages. It's the best resource to understand these functions, or to get documentations regarding these os apis.

On Linux: we use the man command to get this. Or... you could search in google for the man pages.

Remember that not all functions/features found manpage won't be working on Windows. But Windows, Linux, mac etc implements POSIX specified api for many features, and FILE is one of them so we needn't worry about using the guides specific for files.

Example: the manpage for fseek is available on man7.org as well.


https://man7.org/linux/man-pages/man3/fseek.3.html

## Closing a file


Afrer using fopen on a file, operating system holds onto that file, allocates menory, holds on disk for input/output etc. Therefore when we are done with a file, we should release the file or close it, to prevent possible memory leak or other issues.

Closing a file is easy; just do:

```c
// fp is already defined 
fclose(fp);

```

