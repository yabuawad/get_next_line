# get Next line ✧･ﾟ: ( ͡ꈍ ͜ʖ̫ ͡ꈍ ) :･ﾟ✧
get_next_line is a C project where you learn to read from a file descriptor one line at a time, using system calls and a dynamically allocated buffer. This project really teaches you memory management the hard way lol.
## Features
~Reads from any file descriptor (files, stdin, etc.) line by line
~Manages memory carefully to avoid leaks
~Returns NULL when there’s nothing left to read
## Usage
Clone the repository
```Bash
git clone git@github.com:yabuawad/get_next_line.git
cd get_next_line
```
Compile your code
```Bash
cc -Wall -Wextra -Werror -D BUFFER_SIZE=42 get_next_line.c main.c -o gnl
```
Replace main.c with your testing file. BUFFER_SIZE can be any positive integer.
Run the program
```Bash
./gnl example.txt
```
This will read example.txt line by line and print each line.
## How It Works
get_next_line uses:
read() system call to fetch data from the file descriptor
A static buffer to store leftovers between calls
Dynamic memory allocation to return each line properly
Returns NULL when the file ends
It’s basically reading a file in small chunks while carefully managing memory.
## Example
```C
int fd = open("example.txt", O_RDONLY);
char *line;

while ((line = get_next_line(fd)))
{
    printf("%s", line);
    free(line);
}
close(fd);
```
Output:

Line 1 of the file  
Line 2 of the file  
Line 3 of the file  
...
## Notes
Make sure to free every line returned to avoid memory leaks
BUFFER_SIZE affects performance: larger = fewer reads, smaller = more reads
Works with any file descriptor: files, stdin, pipes, etc.
## Lessons Learned
How to handle dynamic memory allocation safely
How to work with system calls in C
Managing buffers and leftovers between function calls
