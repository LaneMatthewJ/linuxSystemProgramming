# CS2750 Final Exam

### True / False 10 Questions 1 point each

1. **True** / False `git` is used as a source control management system. 
2. True / **False** The preprocessing phase of compilation is the phase which breaks the code down to machine code.
3. **True** / False In a stack, when an argument is passed by reference, its value in the stack is a memory location as opposed to its "value".
4. True / **False** To read from a file in a C program using `fopen`, the `a` argument is required. 
5. **True** / False Unit tests in a program are functions that run another function and test its actual output with an expected output.
6. True / **False** When a C program is compiled without a specified output filename, the compiled program is the same name as the C code's filename.
7. True / **False** Signals are caught by using the "catch" function. 
8. **True** / False When a C program forks off a child, a new process is created. 
9. **True** / False Makefiles make use of the `make` utility in linux environments.
10. True / **False** PID is a command to print all jobs stemming from a particular ID. 

### Multiple Choice 10 Questions 4 points each

1. Given the following code, what is the output? 

   ```c
   #include <stdio.h>
   #include <stdlib.h>
   
   #define TRUE 1
   #define FALSE 0
   
   int isGreaterThan(int a, int b){
     return a > b;
   }
   
   void tests() {
     int num1 = 10;
     int num2 = 20;
     int expectedOutput = TRUE; 
     int actualOutput = isGreaterThan(num1, num2);
     
     if (expectedOutput != actualOutput) { 
       printf("Is Greater Than Failed!\n"); 
       exit(1);
     }; 
     
     printf("Is Greater Than Passed!\n");
   }
   
   int main(int argc, char** argv){
     	tests(); 
     	printf("The rest of the file!\n"); 
   }
   ```

   

   - 

     ```
     Is Greater Than Failed!
     ```

   - ```
     Is Greater Than Passed!
     The rest of the file!
     ```

   - ```
     Is Greater Than Passed!
     ```

   - ```
     Is Greater Than Failed!
     The rest of the file!
     ```

2. Given the following code, what is the output: 

   ```c
   #include <stdio.h>
   #include <stdlib.h>
   
   void passByValueAndReference(int a, int* b){
   	a = 500;
     * b = 23; 
   }
   
   int main(int argc, char** argv){
   	int a = 10; 
     int b = 20; 
     int * c = &b; 
   	
     passByValueAndReference(a, c); 
     
     printf("a is:%d \nb is:%d ", a, b);
     
     return EXIT_SUCCESS; 
   }
   ```

   - 

   - 

     ```
     a is:10
     b is:23
     ```

   - ```
     a is:500
     b is:20
     ```

   - ```
     a is:10
     b is:20
     ```

   - ```
     a is:500
     b is:23
     ```

3. Given the following two branches of code in a git repository, what will the subsequent commands be: 
   `index.c`:  `master`

   ```c
   #include <stdio.h>
   #include <stdlib.h>
   
   int main(int argc, char** argv){
     printf("Hello!");
   
     return EXIT_SUCCESS;
   }
   ```

   

   `index.c`: `someBranch`

   

   ```c
   #include <stdio.h>
   #include <stdlib.h>
   
   void printHello() {
     printf("Hello");
   }
   
   int main(int argc, char** argv){
     printHello();
   
     return EXIT_SUCCESS;
   }
   ```


   ```bash
   # Assuming writing this from the master branch: 
    git diff someBranch master
   ```

   

   - ```
     diff --git a/index.c b/index.c
     index 7b14c42..f0fb096 100644
     --- a/index.c
     +++ b/index.c
     @@ -1,12 +1,8 @@
      #include <stdio.h>
      #include <stdlib.h>
     
     -void printHello() {
     -  printf("Hello");
     -}
     -
      int main(int argc, char** argv){
     -  printHello();
     -
     +  printf("Hello!");
     +
        return EXIT_SUCCESS;
      }
     ```

   - ```
     diff --git a/index.c b/index.c
     index f0fb096..7b14c42 100644
     --- a/index.c
     +++ b/index.c
     @@ -1,8 +1,12 @@
      #include <stdio.h>
      #include <stdlib.h>
     
     +void printHello() {
     +  printf("Hello");
     +}
     +
      int main(int argc, char** argv){
     -  printf("Hello!");
     -
     +  printHello();
     +
        return EXIT_SUCCESS;
      }
     ```

   - ```
     diff --git a/index.c b/index.c
     index f0fb096..7b14c42 100644
     --- a/index.c
     +++ b/index.c
     @@ -1,8 +1,12 @@
      #include <stdio.h>
      #include <stdlib.h>
     
     +void printHello() {
     +  printf("Hello");
     +}
     +
     
     +  printHello();
     +
     ```

   - ```
     diff --git a/index.c b/index.c
     index 7b14c42..f0fb096 100644
     --- a/index.c
     +++ b/index.c
     @@ -1,12 +1,8 @@
      #include <stdio.h>
      #include <stdlib.h>
     
     int main(int argc, char** argv){
     +  printf("Hello!");
     +
        return EXIT_SUCCESS;
      }
     ```

     

4. Which of the following code snippets will read from the file `README`: 

   - ```c
     // ....
     FILE * filePointer;
     int character; 
     
     filePointer = fopen("README", "r");
     character = fgetc(filePointer); 
     
     while(character != EOF) {
       printf("%c", character); 
     
       character = fgetc(filePointer); 
     }
     
     fclose(filePointer);
     // ....
     ```

   - ```c
     // ....
     FILE * filePointer;
     int character; 
     
     filePointer = fopen("somefilename.txt", "a");
     character = fgetc(filePointer); 
     
     while(character != EOF) {
       printf("%c", character); 
     
       fprintf(filePointer, "%c", character);
     }
     
     fclose(filePointer);
     // ....
     ```

   - ```c
     // ....
     FILE * filePointer;
     string somestr; 
     
     filePointer = fopen("somefilename.txt");
     somestr = fgetc(filePointer); 
     
     while(character != EOF) {
       fprintf(filePointer, "%c", somestr);
     }
     
     fclose(filePointer);
     // ....
     ```

   - ```c
     // ....
     FILE * filePointer;
     int character; 
     
     filePointer = fopen("somefilename.txt", 1);
     character = fputc(filePointer); 
     
     while(character != EOF) {
       fprintf("somefilename.txt", "%c", character);
     }
     
     fclose(filePointer);
     // ....
     ```

     

5. Which of the following commands will compile and run `someFile.c`  to work with GDB: 

   - ```bash
     gcc gcc -ggdb someFile.c -o someFile
     gdb someFile
     ```

   - ```bash
     gcc -debug someFile.c
     gdb someFile
     ```

   - ```bash
     gcc someFile.c
     gdb a.out
     ```

   - ```bas
     gcc gdb someFile.c
     ```

     

6. Given the following code, which of the following GDB commands will print the stack trace from the function *functionTwo*

   ```c
   #include <stdio.h>
   #include <stdlib.h>
   
   int functionTwo(){
     return 25;
   }
   
   void functionOne(int a){
   	int b = functionTwo();
     int c = a + b; 
     printf("%d + %d is %d", a, b, c);
   }
   
   int main(int argc, char** argv){
   	functionOne(15); 
     
     return EXIT_SUCCESS; 
   }
   ```

   

   - 

     ```
     break functionTwo
     run
     bt
     ```

   - ```
     break functionTwo
     bt
     ```

   - ```
     break functionTwo
     stack
     ```

   - ```
     break functionTwo
     run
     print functionTwo
     ```

     

7. Which of the following code snippets will retrieve the PID of the parent process (assuming all the proper libraries have been brought in)?

   - ```c
     ...
     pid_t someId = getppid(); 
     ...
     ```

   - ```c
     ...
     pid_t someId = getpid(); 
     ...
     ```

   - ```
     ...
     pid_t someId = getParentPID(); 
     ...
     ```

   - ```
     ...
     pid_t someId = getProcessID(); 
     ...
     ```

     

8. Given the following bash commands, which of the following could (given that PIDs are assigned by the kernel) be the output: 
   `takesForever.sh`

   ```bash
   #!/bin/bash
   sleep 500
   ```


   ```bash
   ./takesForever.sh
   ```

   

   - 

     ```
       PID TTY          TIME CMD
       981 pts/2    00:00:00 bash
      2581 pts/2    00:00:00 takeforever.sh
      2584 pts/2    00:00:00 sleep
      2605 pts/2    00:00:00 ps
     ```

   - ```
       PID TTY          TIME CMD
       981 pts/2    00:00:00 bash
      2581 pts/2    00:00:00 takeforever.sh
      2584 pts/2    00:00:00 ps
     ```

   - ```
       PID TTY          TIME CMD
       981 pts/2    00:00:00 bash
      2581 pts/2    00:00:00 takeforever.sh
      2584 pts/2    00:00:00 sleep
     ```

   - ```
       PID TTY          TIME CMD
       981 pts/2    00:00:00 bash
      2581 pts/2    00:00:00 takeforever.sh
     ```

     

9. Given the following code compiles and runs, what will be the output from the subsequent commands:
   `parent.c`

   ```c
   #include<unistd.h>
   #include<sys/types.h>
   #include<stdio.h>
   #include<stdlib.h>
   
   int main(int argc, char** argv) {
     pid_t childPid = fork();  
     printf("Hello!\n");
     if (childPid == 0) {
       char* args[] = {"./child", NULL};
       execv(args[0], args);
     }
     return EXIT_SUCCESS;
   }
   ```

   

   `child.c`

   ```c
   #include<unistd.h>
   #include<sys/types.h>
   #include<stdio.h>
   #include<stdlib.h>
   
   int main(int argc, char** argv) {
     printf("I am a child.\n"); 
   
     return EXIT_SUCCESS; 
   }
   ```

   ```bash
   gcc parent.c -o parent
   gcc child.c -o child
   ./parent
   ```

   

   - 

     ```
     Hello!
     Hello!
     I am a child.
     ```

   - ```
     Hello!
     Hello!
     ```

   - ```
     Hello!
     I am a child.
     ```

   - ```
     Hello!
     ```

10. What is the output of the following command

    ```c
    #include<stdio.h>
    #include<stdlib.h>
    
    int main(int argc, char** argv) {
    	int i = 0; 
      
      pritnf("Loop away!"); 
      while ( i < 5 ); 
      {
        printf("i = %d",i);
        i++; 
      }
      printf("i is %d ", i); 
      return EXIT_SUCCESS; 
    }
    ```

    

    - 

      ```
      Loop away!
      
      ```

    - ```
      Loop away! 
      i = 0
      i = 1
      i = 2
      i = 3
      i = 4
      i is 5
      ```

    - ```
      Loop away! 
      i = 0
      i = 1
      i = 2
      i = 3
      i = 4
      i = 5
      i = 6
      i = 7 
      ...  
      ```

    - ```
      Nothing, the program will fail to compile.
      ```

      

### Short Answer 8 Questions 5 points each

1. Write a void function that takes in the size of an array and an integer pointer, and initializes the array by using only pointer arithmetic. 

   ```c
   void initialize(int SIZE, int * arr){
   	int i; 
     for (i = 0; i < SIZE; i++){
       *arr = 0; 
       arr++; 
     }
   }
   ```

2. Write a function that tests the provided function, and exits with failure if the test fails: 

   ```c
   int getRemainder(int numerator, int denominator) {
     int remainder = numerator % denominator; 
     return remainder; 
   } 
   ```

   

   

   ```c
   void testGetRemainder() {
     int numerator = 7; 
     int denominator = 5; 
     int expected = 2; 
   
     int actual =getRemainder(numerator, denominator); 
     
     if (expected != actual) {
       printf("get remainder failed"); 
       exit(1); 
     }
   }
   ```

3. Draw the Call Stack for the following program `funcs.c` at line 5 (for memory locations, just be consistent): 

   ```c
   #include <stdio.h>
   #include <stdlib.h>
   
   int functionTwo(){
     int f = 25; 
     return f;
   }
   
   void functionOne(int a){
   	int b = functionTwo();
     int c = a + b; 
   }
   
   int main(int argc, char** argv){
   	int x = 10;
     functionOne(x); 
     
     return EXIT_SUCCESS; 
   }
   ```

      

   | Scope     | Name         | Value   | Address |
   | --------- | ------------ | ------- | ------- |
   | function2 | f            | 25      | 127     |
   | function2 | Return Value | 117     | 123     |
   | function2 | Return Line  | Line 10 | 119     |
   | function1 | b            | garbage | 117     |
   | function1 | a            | 10      | 115     |
   | function1 | Return Line  | Line 15 | 112     |
   | main      | x            | 10      | 108     |
   | main      | argv         | Null    | 104     |
   | main      | argc         | 1       | 100     |

   

   

4. Write a short program that reads input from a user and appends it to a file "logfile.txt", only stopping once the user enters the symbol `~`

   ```c
   #include <stdio.h>
   #include <stdlib.h>
   
   int main(int argc, char** argv){
     int characterReadFromStdIn = getchar();
   
     FILE * fileptr = fopen("logfile.txt", "a"); 
     
     do {
   		fprintf(fileptr, '%c', characterReadFromStdIn)
       
       characterReadFromStdIn = getchar()
     } while (characterReadFromStdIn != '~');
   
     fclose("logfile.txt");
     return EXIT_SUCCESS;
   }
   ```

5. Write a short C program takes in shell provided parameters and prints them to the output. 

   ```c
   #include <stdio.h>
   #include <stdlib.h>
   
   int main(int argc, char** argv){
   	int i; 
     for (i = 0; i < argc; i++){
       printf("%s\n", argv[i]);
     }
   
     return EXIT_SUCCESS;
   }
   ```

6. Write a short C program that executes the shell command: 

   ```bash
   ls -la
   ```

   

   ```c
   #include <stdio.h>
   #include <stdlib.h>
   
   int main(int argc, char** argv){
   	system("ls -la"); 
     
     return EXIT_SUCCESS;
   }
   ```

   

7. Write a short C program that captures SIGINT, prints goodbye, and exits the program. 

   ```c
   #include<unistd.h>
   #include<sys/types.h>
   #include<stdio.h>
   #include<stdlib.h>
   #include<signal.h>
   
   void signal_trap(int signal)
   {
     if (signal == SIGINT){
       printf("goodbye\n");
     	exit(0);
     }
   }
   
   
   int main(int argc, char** argv) {
     if (signal(SIGINT, signal_trap) == SIG_ERR)
       printf("\ncan't catch SIGINT\n");
     
     return EXIT_SUCCESS; 
   }
   ```

8. Write a short C program that forks off a child, but then immediately sends a signal to that child with SIGINT. 

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
   
     } else {
       printf("I'm a parent! My pid is %d, and my child's pid is %d \n", getpid(), childPid);
   
       kill(childPid, SIGINT); 
     }
     
     return EXIT_SUCCESS;
   }
   ```

   

### Long Answer 1 Question 10 points

Write a C program that: 

- Takes arguments
  - `-h` for help, which prints a simple "you asked for help" message.
  - `-c` for number of children that the program will fork off.
    - If the argument for `c` does not exist, make its default value 1. 
    - If the argument for `c` is zero, ensure that the program does not fork at all. 
- Forks off `c` children, each of which should then call another program `child.c` with the argument as to which number child it is (i.e. if there are supposed to be 3 child processes, call each child process with a number corresponding to which iteration it's on, so there will be child 1, child 2, and child 3). 
- The parent waits for the children to finish before it finishes. 



**Note: **You can assume that `child.c` exists. There is no need to write that program as well.