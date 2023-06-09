Running the MT Multitasking System: Under Linux, enter
                                      `gcc –m32 t.c s.s`
                                      
 ### Sample Outputs of the MT Multitasking System
![Screenshot 2023-06-09 063821_edited](https://github.com/gamalahmed3265/Operating-Systems/assets/75225936/a9abfeb5-aa9c-42d9-9933-0791a8c3b6bd)



![pipe](https://github.com/gamalahmed3265/Operating-Systems/assets/75225936/16fdee62-b67c-4afa-b7fe-d4cddfc6a880)
![sim](https://github.com/gamalahmed3265/Operating-Systems/assets/75225936/7a3b76d9-5637-4db1-a77b-ef9dae75f55c)










Process management is the set of activities that an operating system performs to create, start, stop, and manage processes. In Unix and Linux, process management is handled by the kernel. The kernel is the core of the operating system, and it is responsible for managing all of the resources on the system, including processes.

The kernel uses a number of tools to manage processes. These tools include:

* **fork():** This system call creates a new process that is a copy of the calling process.
* **exec():** This system call replaces the current process with a new process.
* **wait():** This system call waits for a child process to finish.
* **kill():** This system call sends a signal to a process, which can cause the process to terminate.

Processes can be classified into two types: foreground processes and background processes. Foreground processes are processes that are interactive with the user. Background processes are processes that run in the background and do not require user interaction.

Foreground processes are started by the user at the command line. They are displayed in the foreground of the terminal window. The user can interact with foreground processes by typing commands at the prompt.

Background processes are started by the user with the & character. They are displayed in the background of the terminal window. The user cannot interact with background processes by typing commands at the prompt.

The kernel uses a number of mechanisms to manage the execution of processes. These mechanisms include:

* **Scheduling:** The kernel schedules processes to run on the CPU. The kernel uses a variety of factors to determine which process to run next, such as the priority of the process, the amount of CPU time that the process has used, and the amount of memory that the process is using.
* **Memory management:** The kernel manages the memory that is used by processes. The kernel allocates memory to processes when they are created, and it deallocates memory when processes are terminated.
* **Inter-process communication (IPC):** The kernel provides mechanisms for processes to communicate with each other. These mechanisms include pipes, sockets, and shared memory.

Process management is a complex and important part of Unix and Linux operating systems. The kernel provides a number of tools and mechanisms to manage processes, and these tools and mechanisms are used to ensure that processes run efficiently and safely.




 C program that creates two processes and then waits for the child processes to finish:

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main() {

  // Create a child process
  pid_t pid = fork();

  // If the child process was created, then execute the child code
  if (pid == 0) {

    // Print a message from the child process
    printf("I am the child process\n");

    // Exit the child process
    exit(0);
  }

  // If the parent process was created, then execute the parent code
  else {

    // Wait for the child process to finish
    wait(NULL);

    // Print a message from the parent process
    printf("I am the parent process\n");

    // Exit the parent process
    exit(0);
  }

  return 0;
}
```

This code will create two processes, one child process and one parent process. The child process will print a message and then exit. The parent process will wait for the child process to finish and then print a message and exit.

The code can be modified to create more than two processes, or to have the child processes do something other than print a message.



The dup() and dup2() system calls in Linux are used to duplicate a file descriptor. dup() creates a new file descriptor that refers to the same open file description as the old file descriptor. dup2() creates a new file descriptor that refers to the same open file description as the old file descriptor, and closes the old file descriptor if necessary.

The following table summarizes the differences between dup() and dup2():

| Feature | dup() | dup2() |
|---|---|---|
| File descriptor | Creates a new file descriptor that refers to the same open file description as the old file descriptor. | Creates a new file descriptor that refers to the same open file description as the old file descriptor, and closes the old file descriptor if necessary. |
| Return value | Returns the new file descriptor. | Returns the new file descriptor, or -1 on error. |
| Error codes | EINTR, EBADF, EINVAL, EMFILE, ENFILE, ENOSPC | EINTR, EBADF, EINVAL, EMFILE, ENFILE, ENOSPC, ENOTFD |

example of how to use dup() and dup2():

```c
int main() {

  // Open a file
  int fd = open("file.txt", O_RDONLY);

  // Duplicate the file descriptor
  int new_fd = dup(fd);

  // Close the original file descriptor
  close(fd);

  // Read from the new file descriptor
  char buf[1024];
  read(new_fd, buf, sizeof(buf));

  // Close the new file descriptor
  close(new_fd);

  return 0;
}
```

This code will open the file "file.txt" for reading, duplicate the file descriptor, close the original file descriptor, read from the new file descriptor, and close the new file descriptor.



Sure, here is an example of a C program that uses the `dup2()` system call to duplicate a file descriptor:

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main() {

  // Open a file
  int fd = open("file.txt", O_RDONLY);

  // Duplicate the file descriptor
  int new_fd = dup2(fd, STDOUT_FILENO);

  // Check if the duplicate was successful
  if (new_fd == -1) {
    perror("dup2");
    exit(1);
  }

  // Read from the file descriptor
  char buf[1024];
  read(new_fd, buf, sizeof(buf));

  // Print the contents of the buffer
  printf("%s\n", buf);

  // Close the file descriptor
  close(fd);

  return 0;
}
```

This code will open the file `file.txt` for reading, duplicate the file descriptor, and then read from the new file descriptor. The contents of the file will be printed to the standard output.

The `dup2()` system call can be used to duplicate file descriptors for a variety of purposes. For example, it can be used to redirect the output of a command to a file, or to create a pipe that can be used for communication between two processes.



The dup() and dup2() system calls can be used to duplicate file descriptors for a variety of purposes. For example, they can be used to redirect the output of a command to a file, or to create a pipe that can be used for communication between two processes.



A pipe is a unidirectional communication channel that can be used to pass data between two processes. A named pipe is a special type of pipe that has a name, and can be accessed by any process that knows the name.

Pipes are created using the `pipe()` system call. The `pipe()` system call returns two file descriptors, one for reading from the pipe and one for writing to the pipe.

Named pipes are created using the `mkfifo()` system call. The `mkfifo()` system call creates a new named pipe with the specified name.

To use a pipe, one process opens the pipe for reading and the other process opens the pipe for writing. The process that is writing to the pipe can write data to the pipe, and the process that is reading from the pipe can read data from the pipe.

To use a named pipe, one process opens the named pipe for reading and the other process opens the named pipe for writing. The process that is writing to the named pipe can write data to the named pipe, and the process that is reading from the named pipe can read data from the named pipe.

Pipes and named pipes are a simple and efficient way for processes to communicate with each other. They are often used in shell scripts and in programs that need to communicate with each other.

Here is an example of a C program that uses a pipe to communicate between two processes:

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main() {

  // Create a pipe
  int pipefd[2];
  pipe(pipefd);

  // Fork a child process
  pid_t pid = fork();

  // If the child process was created, then execute the child code
  if (pid == 0) {

    // Close the read end of the pipe
    close(pipefd[0]);

    // Write data to the pipe
    char data[] = "Hello, world!";
    write(pipefd[1], data, strlen(data));

    // Exit the child process
    exit(0);
  }

  // If the parent process was created, then execute the parent code
  else {

    // Close the write end of the pipe
    close(pipefd[1]);

    // Read data from the pipe
    char buffer[1024];
    int bytes_read = read(pipefd[0], buffer, sizeof(buffer));

    // Print the data that was read from the pipe
    printf("%s\n", buffer);

    // Wait for the child process to finish
    wait(NULL);

    // Exit the parent process
    exit(0);
  }

  return 0;
}
```

This code will create two processes, one child process and one parent process. The child process will write the string "Hello, world!" to the pipe, and the parent process will read the string from the pipe and print it to the standard output.











Sure, here is an example of a C program that uses a named pipe to communicate between two processes:

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/stat.h>
#include <sys/types.h>

int main() {

  // Create a named pipe
  int status = mkfifo("myfifo", 0666);

  // Check if the named pipe was created successfully
  if (status < 0) {
    perror("mkfifo");
    exit(1);
  }

  // Fork a child process
  pid_t pid = fork();

  // If the child process was created, then execute the child code
  if (pid == 0) {

    // Open the named pipe for writing
    int fd = open("myfifo", O_WRONLY);

    // Write data to the named pipe
    char data[] = "Hello, world!";
    write(fd, data, strlen(data));

    // Close the named pipe
    close(fd);

    // Exit the child process
    exit(0);
  }

  // If the parent process was created, then execute the parent code
  else {

    // Open the named pipe for reading
    int fd = open("myfifo", O_RDONLY);

    // Read data from the named pipe
    char buffer[1024];
    int bytes_read = read(fd, buffer, sizeof(buffer));

    // Print the data that was read from the named pipe
    printf("%s\n", buffer);

    // Close the named pipe
    close(fd);

    // Wait for the child process to finish
    wait(NULL);

    // Exit the parent process
    exit(0);
  }

  return 0;
}
```

This code will create two processes, one child process and one parent process. The child process will write the string "Hello, world!" to the named pipe, and the parent process will read the string from the named pipe and print it to the standard output.

The named pipe will remain on the filesystem until it is deleted. Any process that knows the name of the named pipe can open it for reading or writing.
