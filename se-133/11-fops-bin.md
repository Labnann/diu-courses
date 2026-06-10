# Binary files
## Writing Binary Files
Once text files are down, understanding binary files are easy.

We write binary files to a function using the fwrite function.


```c
	fwrite( arr: the pointer that points to where from memory we should write,
		s: the amount of bytes we write at once,
		n: how many times we write s bytes to the file,
		fp: the opened file pointer with "wb" mode where the bytes will be written)
```

Consider the following source code:

```c
#include <stdio.h> 
#include <string.h>

struct Rectangle {
	int w;
	int l;
};

int main()
{
	int a[] = {5, 2, 123, 12};

	struct Rectangle r[] = {
		{10, 7},
		{3, 5},
		{12, 17},
		{50, 25}
	};

	FILE *fp = fopen("rectangle.bin" , "wb");
	//fprintf(fp, "text printing");
	fwrite(r, sizeof(struct Rectangle), 4, fp);
}
```

Can you explain what will happen in this code?

The pointer position `r`, `sizeof(struct Rectangle)` amount of data
will be written to file "rectangle.bin" as opened with file pointer fp.

# Can we usually see contents of this rectangle.bin? (Click to Expand)
<details>
  <summary> ## If you don't care about what is inside a binary file, you can skip over. Click me to expand this section.
  </summary>

 
### No, since these are binary files, text editor cannot really open it.

Here is what `vi`, and `nano` sees if this file is opened.

```
^@^@^@^G^@^@^@^C^@^@^@^E^@^@^@^L^@^@^@^Q^@^@^@2^@^@^@^Y^@^@^@
```

On windows, text editor should see something similar.

We can open the file with `hexdump` or `xxd` to see the binary
contents in the file.

I am using `xxd` here.

First column is for easy tracking of where we are looking, last
column is the representation in a text editor. (. means unrepresentable)

Rest of the columns are actual content.

```
00000000: 0a00 0000 0700 0000 0300 0000 0500 0000  ................
00000010: 0c00 0000 1100 0000 3200 0000 1900 0000  ........2.......
```

If you observe carefully, there is 0a (decimal 10), 07 (decimal 7),
03 (decimal 3), 05 (decimal 5), 0c (decimal 12), 11 (decimal 17), 
32 (decimal 50), 19 (decimal 25) in the xxd output.

Each of these numbers take 8 characters to be represnted. Because each
of those numbers are `int` which is 32 bit, ie. needs 8 hexadecimal
values to represent them. As each hex value represents 4 bit.

If it is too confusing for you, we can see the binary values directly.

```
00000000: 00001010 00000000 00000000 00000000 00000111 00000000  ......
00000006: 00000000 00000000 00000011 00000000 00000000 00000000  ......
0000000c: 00000101 00000000 00000000 00000000 00001100 00000000  ......
00000012: 00000000 00000000 00010001 00000000 00000000 00000000  ......
00000018: 00110010 00000000 00000000 00000000 00011001 00000000  2.....
0000001e: 00000000 00000000                                      ..
```

It shows that what we put in that array of ours is exactly saved in 
this file.

This was the array: 

```c
struct Rectangle r[] = {
		{10, 7},
		{3, 5},
		{12, 17},
		{50, 25}
	};

```
</details>

# Perspective

When we deal with a binary file, writing is usually paired with reading. 
Someone creates the file, and someone sees/uses the file.

For example: your cameral will create a binary file:
`your_image.jpg`

And your gallery app, or everyone else you share the image with,
their photoviewer will read the binary file `your_image.jpg`,
process it properly so that you can see the image.

So, we need to read our rectangle.bin too!

## Reading Binary Files

The process is almost similar as before. What happens is the
reverse and you have to use the `fread` function to read the
binary file.


```
	fread( arr: the pointer that points to the memory where we will save whatever we read from fp,
		s: the amount of bytes we read at once,
		n: how many times we read the s bytes,
		fp: the opened file pointer with "rb" mode from where we will read)
```


The following code reads from rectangle.bin and prints one rectangles width and length
to prove that it was able to read successfully.

```c
#include <stdio.h> 

struct Rectangle {
	int w;
	int l;
};

int main()
{

	struct Rectangle r[20];

	FILE *fp = fopen("rectangle.bin" , "rb");
	//fprintf(fp, "text printing");
	fread(r, sizeof(struct Rectangle), 4, fp);

	printf("rectangle 0: w: %d l: %d\n", r[0].w, r[0].l);
}
```
Output:

```
rectangle 0: w: 10 l: 7
```

Can you explain how it worked?
