This project has been created as part of the 42 curriculum by isiboub


# get_next_line

## Description

The get_next_line project consists of implementing a function in C that reads a file line by line from a given file descriptor.

The goal of this project is:

Provide a reusable function that simplifies file reading in C.
Introduce and deeply understand the concept of static variables, which allow data to persist between function calls.

Each call to 'get_next_line(int fd)' returns the next line from the file descriptor, including the terminating '\n' character when present. When there is nothing left to read or an error occurs, the function returns 'NULL'.



## Instructions

### Compilation

The project must be compiled using `cc` with the required flags:

cc -Wall -Wextra -Werror -D BUFFER_SIZE=42 get_next_line.c get_next_line_utils.c

Notes:

* 'BUFFER_SIZE' defines how many bytes are read at a time using the 'read()' system call.

### Usage example

int fd = open("file.txt", O_RDONLY);
char *line;

while ((line = get_next_line(fd)) != NULL)
{
    printf("%s", line);
    free(line);
}
close(fd);


## Algorithm

The implementation relies on a static buffer (stash) that keeps unread data between calls to 'get_next_line'.

### Global logic

1. Read from the file descriptor into a temporary buffer of size 'BUFFER_SIZE'.
2. Append the newly read data to a static variable called the stash.
3. Stop reading as soon as a newline character ('\n') is found or EOF is reached.
4. Extract the first complete line from the stash.
5. Update the stash to keep only the remaining unread data.
6. Return the extracted line.

### Main components

* get_next_line
  Handles input validation, reading logic, and line extraction.

* read_and_fill
  Reads from the file descriptor and appends data to the stash until a newline is found or reading stops.

* extract_line
  Extracts and allocates the next line to return, including the newline if present.

* trim_stash
  Removes the returned line from the stash while preserving remaining data for future calls.

### Helper functions

Custom utility functions are implemented in `get_next_line_utils.c`, such as:

* ft_strlen_gnl
	To calculate the length of a string.
* ft_strchr_gnl
	To return the pointer of the first occurence of a char in a string.
* str_cpy
	To copy a string in another one.
* ft_strjoin_gnl
	To join to strings.

These functions replace standard library utilities, as required by the subject constraints.

## Resources

* 42 Subject PDF – *Get Next Line*
* Linux manual pages: `man 2 read`
* Wikipedia – Static variables in C: [https://en.wikipedia.org/wiki/Static_variable](https://en.wikipedia.org/wiki/Static_variable)
* 42 Guide: [https://42-cursus.gitbook.io/guide/1-rank-01/get_next_line](https://42-cursus.gitbook.io/guide/1-rank-01/get_next_line)

### AI usage

AI tools were used **only as a learning tool**, mainly to:

* Clarify the subject requirements and expected behavior.
* Better understand low-level concepts such as static variables, file descriptors, and the read() system call.

