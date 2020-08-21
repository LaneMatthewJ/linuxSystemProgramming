# System Level Operations with C

When a program executes, it is known as a "process". Each process is assigned a process id (PID) when its first created, and that PID is then used to manage the process throughout its execution. Processes can be in *user mode* and in *kernel mode*. *User mode* for a process is any user written code that is executing, like an application running logic, whereas *kernel mode* is when a process is running low level operations that interact with the kernel of the operating system. 

We've already done a ton of system level programming, however, what we've done was behind the scenes!  A great example of how these calls work is through system input/output! When we use commands such as `putc` and `fopen`, we're using commands provided by the language libraries, and these library functions then make system level calls! When a process is running in *user mode* and makes a call with an I/O function, the process is then interrupted and switched from *user mode* to *kernel mode*. From there, once the required data have been input or output, the process is then switched back from *kernel mode* to *user mode* to then make use of the data retrieved from (or the data sent to) I/O. 

System programming isn't just using calls to the *kernel mode* for I/O processes! It also lets us execute shell commands from within a c program, access the process control table, create brand new processes and let them run off and do their own work, and so much more! 



### Executing Shell Commands

In a c program, you can execute shell commands if necessary with the `system` command: 

`call.c`

```c
#include <stdlib.h>

int main(int argc, char** argv){
	system("touch file_{1,2,3}");
}
```

By making the call to the system command, we're reaching out and running a shell command from within the same working directory as our executing program!

 ```bash
gcc call.c
./a.out
ls
 ```

> a.out  call.c  file_1  file_2  file_3

Curiously, by making these calls, we can also use the power of the shell by using any expansions that your shell can! A downside, though, is that your shell's execution speed will also slow down your program: 

`sleep.c`

```c
#include <stdlib.h>

int main(int argc, char** argv){
	system("sleep 20");
}
```

The `system` command does not spin off an entirely new process to run in the background. The `system` command instead waits to return until the command is finished. There are ways to run processes in the background, which well get to later! Additionally, you cannot retrieve data from what the shell command returned with the command. 



### Process Control 

When processes are created, they are given a virtual address space. The *user space* contains the regions: 

- **Stack** - the stack, where our functions and the references to the variables/parameters/return values/etc.  
- **Data**  - the actual region in which the variables are all stored (i.e. where the addresses actually are). This region contains fixed memory locations for things that are allocated specifically at run time, as well as dynamically allocated memory. 
- **Text** - Machine instructions for the process's functions.
- **Shared** - Shared code with other libraries. 

Processes are additionally granted additional space for the kernel to interact with the process. 



#### Life Cycle

Because of the interactive (with things like I/O) and the multiprogramming nature of linux, each process is either in a state of  **Running**, **Blocked**, **Ready** or it is a **Zombie**. 

##### Running

When a process is "running", that means that it is in the process of being executed. 

##### Blocked 

Also known as *waiting*, this is when the processes is waiting for something, such as a response from user input, a call from another program, a system call, etc. Once a program is unblocked, it can then return to the *ready* state. 

##### Ready

A process is ready when it is not blocked, it can be scheduled to return to *running* immediately. 

##### Zombie

When a process finishes, it becomes a zombie. The process itself dies, but it leaves behind data concerning its exit status and other statistics. 



### Process Table

All processes are managed by the *kernel* through the **process table**. Each process is has its own entry, distinguished by the process's id (PID), its status, and other data. To see data concerning a process, use the `ps` command in your command line: 

```bash
ps
```

>   PID TTY          TIME CMD
>
>  2837 pts/0    00:00:00 bash
>
>  6071 pts/0    00:00:00 ps

 Curiously, we see `bash` and `ps`. This is because we're currently interacting with the computer through the `bash` command line, and we just happened to execute the `ps` command through bash, so we not only see the program we're interacting with (i.e. bash), but also the command that lets us view the processes to begin with (i.e. ps). 

Let's flesh this out a little more: 

```bash
sleep 10 &
ps
```

> [1] 6658
>
> PID TTY          TIME CMD
>
>  2837 pts/0    00:00:00 bash
>
>  6658 pts/0    00:00:00 sleep
>
>  6686 pts/0    00:00:00 ps

So not only do we see our original `bash` (note, with the same `PID` as above, since the shell never stopped), we also now see `sleep` with the `PID` that was output when we placed it in the background and `ps` which we called to see the processes in the first place! 

The `ps` comand can also show us a full format listing: 

```bash
sleep 10 &
ps -f 
```

> UID        PID  PPID  C STIME TTY          TIME CMD
>
> mjlny2    2837  2836  0 21:07 pts/0    00:00:00 -bash
>
> mjlny2    7212  2837  0 21:47 pts/0    00:00:00 sleep 10
>
> mjlny2    7236  2837  0 21:47 pts/0    00:00:00 ps -f

Above, we see UID, PID, PPID, C,  STIME,  TTY,  TIME, and CMD. What are these? 

- **UID** - The id of the user who started the process
- **PID** - The process ID
- **PPID** - The process ID of the process's parent. Notice that the PPID of both `sleep` and `ps -f` is 2837, the same PID as `bash`? 
- **C** - Cpu usage and scheduling information
- **STIME** - The start time of the process. 
- **TTY** - The terminal associated with the process. 
- **CMD** - The name of the process's command. 

All processes are started from other processes, all the way back up to the root process. How do we do with with C programs? 



### Fork

When running a C program, you may wish to spin off another process to execute in the background, to do this, you'll want to use the `fork` command. When `fork` is called, the program calling it is referred to as the `parent`, and the new process that starts running is referred to as the `child`. Once the `fork` process is called, both parent and child simultaneously from the exact same point in the code with the exact same values up to that point.  

The `fork` command returns the child process's PID so that the parent process can signal to the child process. In the child process, `fork` returns a value, but it returns 0. It is possible for `fork` to fail, and if it does so, it returns a -1. 

Let's create a file that will fork off a child, and then have both parent and child write to a file: 

`forking.c`

```c
#include<unistd.h>
#include<sys/types.h>
#include<stdio.h>
#include<stdlib.h>

int main(int argc, char** argv) {

  pid_t childPid = fork();  // This is where the child process splits from the parent

  if (childPid == 0) {
    printf("I am a child! My parent's PID is %d, and my PID is %d\n", getppid(), getpid());
  } else {
    printf("I'm a parent! My pid is %d, and my child's pid is %d \n", getpid(), childPid);
  }

  return EXIT_SUCCESS;
}
```

In the above code, we have a parent forking off a child at line 8. From there, a new child process is created! We then access the child process's PID through using what was returned from `fork`. We can also see that the processes can access their own PIDs by using the `getpid` command, and they can even look upwards to see their parents' PIDs by using `getppid`. 

Suppose 



```c
#include<unistd.h>
#include<sys/types.h>
#include<stdio.h>
#include<stdlib.h>

void printArray(int * arr, int size, FILE * outputFilePointer, char* executionContext) {
	fprintf(outputFilePointer, "%s's array says: ", executionContext);

  int i;
  for (i = 0; i < size; i++) {
    fprintf(outputFilePointer, "%d ", arr[i]); 
  }
  fprintf(outputFilePointer, "\n"); 
}

void mutateArray(int *arr, int size, int multiplier) {
	int i;
  for (i = 0; i < size; i++) {
    arr[i] = arr[i] * multiplier; 
  }
}

int main(int argc, char** argv) {
  char* filename = "logfile.txt";
  char* executionContext = "parent";
  int SIZE = 10; 
	int someArray[SIZE] = { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9}; 
  
  pid_t childPid = fork();  // This is where the child process splits from the parent

  if (childPid == 0) {
    printf("I am a child! My parent's PID is %d, and my PID is %d\n", getppid(), getpid());

    executionContext = "child";
    
    mutateArray(someArray, SIZE, 3); 
  } else {
    printf("I'm a parent! My pid is %d, and my child's pid is %d \n", getpid(), childPid);

    sleep(1); 
    mutateArray(someArray, SIZE, 1); 
  }


  FILE * outputFilePointer;

  outputFilePointer = fopen(filename, "a");

  if (outputFilePointer == NULL) {
    printf("Bad file! %s cannot be opened", filename);

    return EXIT_FAILURE;
  }

  printArray(someArray, SIZE, outputFilePointer, executionContext); 

  fclose(outputFilePointer);

  return EXIT_SUCCESS;
}
```

What's happening in the above code!? We `fork`, and then immediately start accessing an array to mutate it. Both parent and child mutate their arrays in different ways. We then choose to write to a file! What's curious is that, depending on the speed of the system, it's possible for this output to be intertwined (however, for this specific example it's relatively unlikely since these processes are so short). Entirely new address spaces are used, so we don't ever have to worry about overwriting! 



### Exec 

It's also entirely possible for programs to execute other C programs by overlaying themselves with an executable file! This can be done with the `exec` library functions! With the exec functions, you can still pass arguments in just as if you were working through the command line. Let's create two files: 

`child.c`

```c
#include<unistd.h>
#include<sys/types.h>
#include<stdio.h>
#include<stdlib.h>

int main(int argc, char** argv) {
  printf("Hello from Child.c!\n"); 
  printf(" I got %d arguments: \n", argc);
  
  int i; 
  for (i =0; i < argc; i++) 
    printf("%s ", argv[i]); 

  printf("\nChild is now ending.\n"); 
  
  return EXIT_SUCCESS; 
}
```

`parent.c`

```c
#include<unistd.h>
#include<sys/types.h>
#include<stdio.h>
#include<stdlib.h>


int main(int argc, char** argv) {
  pid_t childPid = fork();  // This is where the child process splits from the parent

  if (childPid == 0) {
    printf("I am a child! My parent's PID is %d, and my PID is %d\n", getppid(), getpid());

    char* args[] = {"./child", "Hello", "there", "exec", "is", "neat", 0};
      (args[0], args);

  } else {
    printf("I'm a parent! My pid is %d, and my child's pid is %d \n", getpid(), childPid);

    sleep(1);

  }

  printf("Parent is now ending.\n");
  return EXIT_SUCCESS;
}
```

So, when we execute this: 

```bash
gcc child.c -o child
gcc parent.c
./a.out
```

> I'm a parent! My pid is 15539, and my child's pid is 15540
>
> I am a child! My parent's PID is 15539, and my PID is 15540
>
> Hello from Child.c!
>
>  I got 6 arguments:
>
> ./child Hello there exec is neat
>
> Child is now ending
>
> Parent is now ending.

In the above code, what's happening? So, we're forking off a child process just like we did last time, however, what we're doing immediately after is sending the process to an entirely different executable! Additionally, we're sending it with some arguments to take over! This will be incredibly useful if you ever need to send special flags to your child process's programs! Notice at the end of the array, we have a 0?  Try removing that and see what happens! Because we're sending in an array of strings, we need our "string" of arguments to have an end, so we make sure that the new program knows we're done! 



### Synchronization! 

When you fork off child processes, you generally want to make sure that your parent process waits until the child processes are finished. It is possible to just ignore them, but often enough you'll want to know that your child processes have finished, and you can do that with the `wait` command. This command waits until children are in a zombie state, and reacts! 

`wait` sleeps until a child process enters the zombie state, and either returns -1 if there are no other child processes, OR `wait` selects a zombie child and frees that child's process table slot for use for another program, and then stores that child's termination status in `*t_status` and returns the child's PID. 

`parent.c`

```c
#include<unistd.h>
#include<sys/types.h>
#include<stdio.h>
#include<stdlib.h>


int main(int argc, char** argv) {
  pid_t childPid = fork();  // This is where the child process splits from the parent

  if (childPid == 0) {
    printf("I am a child! My parent's PID is %d, and my PID is %d\n", getppid(), getpid());

    char* args[] = {"./child", "Hello", "there", "exec", "is", "neat", 0};
      execv(args[0], args);

  } else {
    printf("I'm a parent! My pid is %d, and my child's pid is %d \n", getpid(), childPid);

  }

    int status;

  printf("waiting for my children\n");
  wait(&status);
    printf("Parent waited until the child ended with %d\n", WEXITSTATUS(status));

  printf("Parent is now ending.\n");
  return EXIT_SUCCESS;
}
```

Above, we're using the `wait` command to wait for our child! We've passed in the address of status so that we can call it with the `WEXITSTATUS` function in order to get the exit status of our child process! 

Now, if we run this: 

```bash
gcc parent.c
./a.out
```

> I'm a parent! My pid is 16909, and my child's pid is 16910
>
> waiting for my children
>
> I am a child! My parent's PID is 16909, and my PID is 16910
>
> Hello from Child.c!
>
>  I got 6 arguments:
>
> ./child Hello there exec is neat
>
> Child is now ending
>
> Parent waited until the child ended with 0
>
> Parent is now ending.

Our parent sat and waited until the child process finished, and then finished ourselves. 



### Terminating a Process

Many, if not most of our programs so far have all ended once the main function ended with a `return EXIT_SUCCESS` or possibly a `return 0`. This works fine and well, but it is also possible for the program to exit with the command `exit(status)` where `status` is an integer value, or by receiving an interrupt or a signal! 



### Signals and Interrupts

We've worked with interrupts before! Events that come from other programs or user input can act as signals for one of our programs to execute a series of commands. These commands are not unlike our signal capturing with bash! Processes typically have a default actions with signals, but we can overwrite those! 

#### Signal Sending

We can send signals from within our programs to achieve some goal. Suppose we had a child process that was taking far too long. We could send a signal to our child process and make sure it ended! To do this, we need to make sure that we include the header `#include<signal.h>` before we try to use the system calls though! 

`child.c`

```c
#include<unistd.h>
#include<sys/types.h>
#include<stdio.h>
#include<stdlib.h>

int main(int argc, char** argv) {
  printf("Hello from Child.c!\n"); 
  printf(" I got %d arguments: \n", argc);
  
  int i; 
  for (i =0; i < argc; i++){ 
    printf("%s ", argv[i]);
	  sleep(2);
  }
  
  printf("\nChild is now ending.\n"); 
  
  return EXIT_SUCCESS; 
}
```

`parent.c`

```c
#include<unistd.h>
#include<sys/types.h>
#include<stdio.h>
#include<stdlib.h>
#include<signal.h>

int main(int argc, char** argv) {
  pid_t childPid = fork();  // This is where the child process splits from the parent

  if (childPid == 0) {
    printf("I am a child! My parent's PID is %d, and my PID is %d\n", getppid(), getpid());

    char* args[] = {"./child", "Hello", "there", "exec", "is", "neat", 0};
      execv(args[0], args);

  } else {
    printf("I'm a parent! My pid is %d, and my child's pid is %d \n", getpid(), childPid);

  }

	sleep(5); 
  kill(childPid, SIGINT); 
  
  return EXIT_SUCCESS;
}
```

In the above code, all we changed was adding a sleep to our child's loop, and then including our signal library in `parent.c`, and then adding a `sleep(5)` and a `kill` command at lines 21 and 22! 

If we run this code: 

```bash
gcc child.c -o child
gcc parent.c
./a.out
```

> I'm a parent! My pid is 18519, and my child's pid is 18520
>
> I am a child! My parent's PID is 18519, and my PID is 18520
>
> Hello from Child.c!
>
>  I got 6 arguments:

Our parent got tired of waiting and killed the child process before it was finished! 

#### Trapping a Signal

It's all fine and dandy to throw a sigint at a program we want to end, however, sometimes you may wish to do something more, like print one last bit of logs, deallocate memory, closing a file pointer, etc. There are any number of things you might want to do before exiting a program. Let's change our child program to capture sigint: 

`child.c`

```c
#include<unistd.h>
#include<sys/types.h>
#include<stdio.h>
#include<stdlib.h>
#include<signal.h>

void signal_trap(int signal)
{
  if (signal == SIGINT){
    printf("received SIGINT\n");
  	printf("if I had arrays, I could deallocate that memory\n"); 
  	printf("for now, I'll just say goodbye cruel world");
  	exit(0);
  }
}


int main(int argc, char** argv) {
  if (signal(SIGINT, signal_trap) == SIG_ERR)
    printf("\ncan't catch SIGINT\n");
  
  printf("Hello from Child.c!\n"); 
  printf(" I got %d arguments: \n", argc);
  
  int i; 
  for (i =0; i < argc; i++){ 
    printf("%s ", argv[i]);
	  sleep(2);
  }
  
  printf("\nChild is now ending.\n"); 
  
  return EXIT_SUCCESS; 
}
```

Now, if we recompile our child program, and then run the parent, let's see what we get! 

```bash
gcc child.c -o child
./a.out.  # << calling the previously compiled parent
```

> I'm a parent! My pid is 20123, and my child's pid is 20124
>
> I am a child! My parent's PID is 20123, and my PID is 20124
>
> Hello from Child.c!
>
>  I got 6 arguments:
>
> ./child Hello there received SIGINT
>
> if I had arrays, I could deallocate that memory
>
> for now, I'll just say goodbye cruel world















