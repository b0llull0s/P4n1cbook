---
icon: shovel
---

# Reverse Engineering

{% hint style="info" %}
## <mark style="color:purple;">Binaries</mark>

### <mark style="color:orange;">`C Fundamentals`</mark>

<mark style="color:purple;">Before you start reversing binaries and analyzing compiled code, it's crucial to have a solid understanding of the foundational concepts that will come up repeatedly during the process:</mark>

* ### <mark style="color:purple;">Library Functions</mark>
  * <mark style="color:purple;">**Memory Management**</mark><mark style="color:purple;">:</mark>
    * <mark style="color:orange;">**`malloc()`**</mark><mark style="color:purple;">:  Allocates a block of memory of a specified size. It returns a pointer to the first byte of the allocated memory, or</mark> <mark style="color:orange;">**`NULL`**</mark> <mark style="color:purple;">if the allocation fails.</mark>
    * <mark style="color:orange;">**`free()`**</mark><mark style="color:purple;">: Releases a block of memory that was previously allocated by</mark> <mark style="color:orange;">**`malloc()`**</mark> <mark style="color:purple;">or</mark> <mark style="color:orange;">**`calloc()`**</mark><mark style="color:purple;">. Failing to free memory leads to memory leaks.</mark>
    * <mark style="color:orange;">**`realloc()`**</mark><mark style="color:purple;">: Resizes a previously allocated block of memory. It can expand or shrink the memory block. If the reallocation is successful, it returns a pointer to the new memory location.</mark>
  * <mark style="color:purple;">**String Manipulation**</mark><mark style="color:purple;">:</mark>
    * <mark style="color:orange;">**`strcpy()`**</mark><mark style="color:purple;">: Copies a null-terminated string from the source to the destination. It is unsafe and can lead to buffer overflows if not used carefully.</mark>
    * <mark style="color:orange;">**`strncpy()`**</mark><mark style="color:purple;">: Copies up to</mark> <mark style="color:orange;">**`n`**</mark> <mark style="color:purple;">characters from one string to another. It is safer than</mark> <mark style="color:orange;">**`strcpy()`**</mark> <mark style="color:purple;">as it prevents buffer overflows (but still requires caution to avoid truncating strings).</mark>
    * <mark style="color:orange;">**`strcmp()`**</mark><mark style="color:purple;">: Compares two strings lexicographically. It returns</mark> <mark style="color:orange;">**`0`**</mark> <mark style="color:purple;">if the strings are identical, a positive value if the first string is lexicographically greater, or a negative value if the second string is greater.</mark>
    * <mark style="color:orange;">**`strlen()`**</mark><mark style="color:purple;">: Returns the length of a null-terminated string, excluding the null terminator. It’s used frequently to determine the size of buffers or strings.</mark>
  * <mark style="color:purple;">**File I/O**</mark><mark style="color:purple;">:</mark>
    * <mark style="color:orange;">**`fopen()`**</mark><mark style="color:purple;">: Opens a file for reading, writing, or both, depending on the mode. It returns a pointer to a</mark> <mark style="color:orange;">**`FILE`**</mark> <mark style="color:purple;">object that represents the open file.</mark>
    * <mark style="color:orange;">**`fclose()`**</mark><mark style="color:purple;">: Closes an open file. Always ensure files are closed after use to avoid memory leaks or file locking issues.</mark>
    * <mark style="color:orange;">**`fread()`**</mark><mark style="color:purple;">: Reads data from an open file stream into a buffer. The size of the data read is specified by the user.</mark>
    * <mark style="color:orange;">**`fwrite()`**</mark><mark style="color:purple;">: Writes data to an open file stream from a buffer.</mark>
  * <mark style="color:purple;">**Input/Output**</mark><mark style="color:purple;">:</mark>
    * <mark style="color:orange;">**`printf()`**</mark><mark style="color:purple;">: Prints formatted output to the standard output (</mark><mark style="color:orange;">**`stdout`**</mark><mark style="color:purple;">). It supports various format specifiers for formatting strings, integers, floating-point numbers, etc.</mark>
    * <mark style="color:orange;">**`scanf()`**</mark><mark style="color:purple;">: Reads formatted input from the standard input (</mark><mark style="color:orange;">**`stdin`**</mark><mark style="color:purple;">). It allows the user to provide input in a specified format.</mark>
    * <mark style="color:orange;">**`puts()`**</mark><mark style="color:purple;">: Writes a string to the standard output (</mark><mark style="color:orange;">**`stdout`**</mark><mark style="color:purple;">) followed by a newline. It is a simpler version of</mark> <mark style="color:orange;">**`printf()`**</mark><mark style="color:purple;">.</mark>
    * <mark style="color:orange;">**`getchar()`**</mark><mark style="color:purple;">: Reads a single character from the standard input (</mark><mark style="color:orange;">**`stdin`**</mark><mark style="color:purple;">). It is often used in simple input scenarios.</mark>
* ### <mark style="color:purple;">**System Calls**</mark>
  * <mark style="color:purple;">**Process Management**</mark><mark style="color:purple;">:</mark>
    * <mark style="color:orange;">**`fork()`**</mark><mark style="color:purple;">: Creates a new process by duplicating the calling process. The new process is a child process and has its own memory space.</mark>
    * <mark style="color:orange;">**`execvp()`**</mark><mark style="color:purple;">: Replaces the current process with a new one. It executes the command specified by the argument (often used in combination with</mark> <mark style="color:orange;">**`fork()`**</mark><mark style="color:purple;">).</mark>
    * <mark style="color:orange;">**`exit()`**</mark><mark style="color:purple;">: Terminates the calling process and returns an exit status to the operating system. It is often used at the end of a program or when a fatal error occurs.</mark>
    * <mark style="color:orange;">**`setuid()`**</mark><mark style="color:purple;">: Sets the user ID (</mark><mark style="color:orange;">**`UID`**</mark><mark style="color:purple;">) for the calling process. A common use is to escalate privileges (e.g., setting the</mark> <mark style="color:orange;">**`UID`**</mark> <mark style="color:purple;">to</mark> <mark style="color:orange;">**`0`**</mark> <mark style="color:purple;">for root privileges).</mark>
    * <mark style="color:orange;">**`getuid()`**</mark><mark style="color:purple;">: Returns the</mark> <mark style="color:orange;">**`UID`**</mark> <mark style="color:purple;">of the calling process.</mark>
  * <mark style="color:purple;">**Memory Management**</mark><mark style="color:purple;">:</mark>
    * <mark style="color:orange;">**`mmap()`**</mark><mark style="color:purple;">: Maps files or devices into memory. It is commonly used for memory-mapped files or to allocate large blocks of memory for a program.</mark>
    * <mark style="color:orange;">**`brk()`**</mark><mark style="color:purple;">: Used to control the end of the data (heap) segment. It’s an older memory management function, and it is rarely used in modern programs.</mark>
    * <mark style="color:orange;">**`sbrk()`**</mark><mark style="color:purple;">: Moves the program’s break (end of the data segment) by a specified increment. Like</mark> <mark style="color:orange;">**`brk()`**</mark><mark style="color:purple;">, it is an older memory management system call and not commonly used in newer programs.</mark>
  * <mark style="color:purple;">**File Operations**</mark><mark style="color:purple;">:</mark>
    * <mark style="color:orange;">**`open()`**</mark><mark style="color:purple;">: Opens a file (or creates it if it doesn't exist) for reading, writing, or both. Returns a file descriptor, which is used for other operations (e.g.,</mark> <mark style="color:orange;">**`read()`**</mark><mark style="color:purple;">,</mark> <mark style="color:orange;">**`write()`**</mark><mark style="color:purple;">).</mark>
    * <mark style="color:orange;">**`read()`**</mark><mark style="color:purple;">: Reads data from a file descriptor into a buffer. Returns the number of bytes read, or</mark> <mark style="color:orange;">**`-1`**</mark> <mark style="color:purple;">on error.</mark>
    * <mark style="color:orange;">**`write()`**</mark><mark style="color:purple;">: Writes data from a buffer to a file descriptor. Returns the number of bytes written, or</mark> <mark style="color:orange;">**`-1`**</mark> <mark style="color:purple;">on error.</mark>
    * <mark style="color:orange;">**`close()`**</mark><mark style="color:purple;">: Closes a file descriptor, freeing up system resources associated with it.</mark>
* ### <mark style="color:purple;">Signals</mark>
  * <mark style="color:purple;">Used to handle asynchronous events in a process, such as interruptions, timeouts, or the termination of child processes. They allow programs to respond to events without explicitly checking for them in the main execution flow:</mark>
    * <mark style="color:orange;">**`signal()`**</mark><mark style="color:purple;">: Sets a handler function for a particular signal. For example, you can set a custom handler for</mark> <mark style="color:orange;">**`SIGINT`**</mark> <mark style="color:purple;">to catch interrupt signals (like</mark> <mark style="color:orange;">**`Ctrl+C`**</mark><mark style="color:purple;">).</mark>
    * <mark style="color:orange;">**`kill()`**</mark><mark style="color:purple;">: Sends a signal to a process. It can be used to terminate processes or trigger specific handlers.</mark>
    * <mark style="color:orange;">**`SIGCHLD`**</mark><mark style="color:purple;">: Sent to a parent process when a child process terminates. This is useful for handling child process lifecycles (e.g., in process management).</mark>
    * <mark style="color:orange;">**`SIGINT`**</mark><mark style="color:purple;">: Sent when a user interrupts a process (e.g., pressing</mark> <mark style="color:orange;">**`Ctrl+C`**</mark><mark style="color:purple;">). It is typically used to terminate processes.</mark>
    * <mark style="color:orange;">**`SIGSEGV`**</mark><mark style="color:purple;">: Sent when a program attempts to access memory that it is not allowed to (segmentation fault). It usually indicates a bug in the program, like a null pointer dereference.</mark>
    * <mark style="color:orange;">**`SIGKILL`**</mark><mark style="color:purple;">: A signal that immediately terminates a process. Unlike</mark> <mark style="color:orange;">**`SIGTERM`**</mark><mark style="color:purple;">, the process cannot catch or ignore</mark> <mark style="color:orange;">**`SIGKILL`**</mark><mark style="color:purple;">**.**</mark>

***

<mark style="color:purple;">**Understanding**</mark>**&#x20;**<mark style="color:orange;">**`ltrace`**</mark>**&#x20;**<mark style="color:purple;">**Outputs**</mark>

<mark style="color:purple;">The quickest way to get a feel for what a binary is doing is to run it with</mark> <mark style="color:orange;">**`ltrace`**</mark><mark style="color:purple;">, which will print all the library calls it’s making:</mark>

```sh
ltrace <BINARY> id
```

<mark style="color:purple;">By analyzing these outputs, you can infer the program's behavior, detect privilege escalation, identify input validation mechanisms, and spot security features like whitelists and blacklists:</mark>

* <mark style="color:orange;">**`UID`**</mark>**&#x20;**<mark style="color:purple;">**Checks and Privilege Escalation**</mark>
  * <mark style="color:purple;">The</mark> <mark style="color:orange;">**`setuid(0)`**</mark> <mark style="color:purple;">function call attempts to set the</mark> <mark style="color:orange;">**`UID`**</mark> <mark style="color:purple;">to</mark> <mark style="color:orange;">**`root`**</mark><mark style="color:purple;">. If it succeeds returns</mark> <mark style="color:orange;">**`0`**</mark><mark style="color:purple;">.</mark>&#x20;
  * <mark style="color:purple;">A failure (</mark><mark style="color:orange;">**`-1`**</mark><mark style="color:purple;">) may indicate the program requires elevated permissions to execute certain operations.</mark>
* <mark style="color:purple;">**Whitelists/Blacklists**</mark>
  * <mark style="color:orange;">**`strncmp`**</mark> <mark style="color:purple;">or</mark> <mark style="color:orange;">**`strcmp`**</mark> <mark style="color:purple;">calls are used to compare input against predefined strings. A return value of</mark> <mark style="color:orange;">**`-1`**</mark> <mark style="color:purple;">indicates a mismatch.</mark>
  * <mark style="color:orange;">**`strcspn`**</mark> <mark style="color:purple;">calls are used to check for forbidden characters (e.g.,</mark> <mark style="color:orange;">**`|`**</mark><mark style="color:purple;">,</mark> <mark style="color:orange;">**`&`**</mark><mark style="color:purple;">,</mark> <mark style="color:orange;">**`>`**</mark><mark style="color:purple;">, which could be part of command injection attempts).</mark>
* <mark style="color:purple;">**File Operations and File Descriptors**</mark>
  * <mark style="color:purple;">Look for files related to user credentials, configuration, or logs.</mark>
* <mark style="color:purple;">**External Command Execution**</mark>
  * <mark style="color:purple;">Calls to</mark> <mark style="color:orange;">**`system()`**</mark><mark style="color:purple;">,</mark> <mark style="color:orange;">**`execvp()`**</mark><mark style="color:purple;">, or similar functions: These often indicate the program is executing shell commands.</mark>
  * <mark style="color:purple;">Input passed to these commands: If user input directly influences these calls, it might indicate an injection vulnerability.</mark>
* <mark style="color:purple;">**Signals and Inter-Process Communication**</mark>
  * <mark style="color:purple;">Signals like</mark> <mark style="color:orange;">**`SIGCHLD`**</mark><mark style="color:purple;">,</mark> <mark style="color:orange;">**`SIGSEGV`**</mark><mark style="color:purple;">, or</mark> <mark style="color:orange;">**`SIGKILL`**</mark> <mark style="color:purple;">in the output.</mark>
  * <mark style="color:purple;">Use of</mark> <mark style="color:orange;">**`kill()`**</mark> <mark style="color:purple;">to manage or terminate processes, which can indicate how the program interacts with other processes.</mark>
{% endhint %}

