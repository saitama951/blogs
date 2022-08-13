# Headers and Libraries

Header files and libraries are common in programming languages, and most of you
would know what they mean. Yet some get confused by the terms itself.


## Header file vs Library:
A header file consists of all the prototypes, symbols and macros of a library
while a library consists of all the definitions of the functions. Now in linux,
we can say a header file could be ```<stdio.h>```and the corresponding library would
be ```libc.so.6```. You can find the header file at ```/usr/include/``` and find the libraries
at ```/usr/lib/```. And some libraries needs be specifically be linked when with gcc
while compiling the program. So let's say you write a program relating to some
mathematical operation and use some math functions (```sqrt()```,```pow()```,..) and then 
while compiling the program you have to add the ```-lm``` flag. That's nothing but 
```libm.so.6``` and similarly we have to specify the thread library (```-lpthread```) 
while writing out multi-threaded programs.


While writing programs, the first line is usually the header file.  The declaration can 
be done like ```#include <stdio.h>``` or like ```#include"stdio.h"```.  Now the 
question arises, what would be difference between these two? One would say just the 
angular brackets and the quotation marks. But what do they actually signify?


To keep it simple, the angular brackets(```< >```) tells the compiler to search 
the particular header file in the default directory (```/usr/include/```),
while the double quotations(```" "```) tips the compiler to search for the header
file in the current directory and if it doesn't find it there then it tries
to find it in the default path (```/usr/include```). quotations are mostly used for
user defined header files and libraries but if you place your header files and
libraries in the default path (```/usr/include/``` and ```/usr/lib/```) then the angle
brackets should just work fine with it (PS: don't forget to link the library
while compiling).


## Making our own ```printf()```:
Okay let's see some examples and try to define our own ```printf()```.
First lets declare the prototype of our own ```printf()``` in ``` stdio.h```

### `stdio.h`

```c
void printf(char str[]);

```

And now define our function within ```main.c```. keep in mind that ```main.c```
and our ```stdio.h``` should in the same level or directory.

### `main.c`

```c
#include "stdio.h"
#include "fcntl.h"

void printf(char str[])
{
	int fd = open("/dev/stdout",O_WRONLY);
	int i;
	for(i=0;i<3;i++)
	{
		write(fd,str[i],1);
	}
	close(fd);
}
void main()
{
	printf("BYE. running default printf\n");
}
```

### Output main:
![output main](images/ss.png)


For demonstration purposes I have printed just the first three characters
so that we can verify that our custom ```printf()``` is been executed and not the
default one. 

## Explaining the code:

Let's see exactly did we did right now. As we are defining out own ```printf```
, we can't use the default ```printf()``` to print the output to the console.
So what we did is opened a file which exists within the linux operating system
```/dev/stdout```. Now ```stdout, stdin, stderr``` are files which are responsible for
the I/O operations within the system. writing something to ```stdout``` would display
the characters to the console. Similarly, writing something to ```stdin``` would mean 
taking input from the console. And finally, ```stderr``` is responsible for displaying error
to the console. So here we open the the ```stdout``` file and only write the first three
characters of the passed argument into the file and after closing the file the output is
displayed to the console.


### Output error:
![output error](images/ss1.png)


Now, if we remove the ```stdio.h``` from the directory and then re-compile the program,
we would get an error of conflicting types. This is because the compiler couldn't find a 
```stdio.h``` header file in the current directory so it goes to the default path 
```/usr/include/```, and there it finds the header file. But an issue arises, as our function
doesn't matches the prototype defined in the header file, and hence
an error message gets displayed.


If you need any clarifications or have suggestions in the blog feel free to reach out :)

The blog page is open source, and you are free to open a pull request on 
[GitHub!](https://github.com/saitama951/blogs/blob/main/src/chapter_1.md)
