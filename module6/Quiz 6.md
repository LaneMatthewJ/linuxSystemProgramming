# Quiz 6

1. Which of the following commands will run the compiled code: 
   `helloWorld.c`

   ```c
   #include <stdio.h>
   
   int main(int argc, char** argv){
     printf("Hello World\n"); 
     
     return 0;
   }
   ```

   ```bash
   gcc helloWorld.c
   ```

   - ```bash
     ./a.out
     ```

   - ```bash
     ./helloWorld.c
     ```

   - ```bash
     helloWorld.c
     ```

   - ```bash
     ./hello
     ```

     

2. Given the following code, what is the output? 

   ```c
   #include <stdio.h>
   
   #ifdef EXIT_FAILURE
   #define FAILURE EXIT_FAILURE
   #else
   #define FAILURE 20
   #endif
   
   int main(int argc, char** argv){
     printf("Hello World\n");
     printf("FAILURE is %d", FAILURE);
     return FAILURE;
   }
   ```

   ```bash
   gcc macro.c -o macro
   ./macro
   ```

   

     - ```bach
       Hello World
       FAILURE is 20
       ```

     - ```bash
       FAILURE is 1
       ```

     - ```bash
       Hello World
       FAILURE is 1
       ```

     - ```bash
       Failure is 20
       ```

       

3. Assuming the following code is compiled, what is the output of the following commands: 
   `arguments.c`

   ```c
   #include <stdio.h>
   #include <stdlib.h>
   
   int main(int argc, char** argv){
   
     int i; 
   	for(i = 0; i < argc; i++){
       printf("Argument %d is %s\n", i, argv[i]); 
     }
     
     return EXIT_SUCCESS; 
   }
   ```
   
```bash
   gcc arguments.c -o doArguments
./doArguments here are some arguments
```



   - 
     
     ```bash
     Argument 0 is ./doArguments
     Argument 1 is here
     Argument 2 is are
     Argument 3 is some
   Argument 4 is arguments
   ```
   
   - ```bash
     Argument 0 is ./a.out
     Argument 1 is here
     Argument 2 is are
     Argument 3 is some
     Argument 4 is arguments
     ```
   
   - ```bash
     here are some arguments
     ```
   
   - ```bash
     here
     are
     some
     arguments
     ```
   
     

4. Given the following code, from where is the input coming: 

   ```c
   #include <stdio.h>
   #include <stdlib.h>
   
   int main(int argc, char** argv){
     int someChar = getchar();
   
   	 do {
      putchar(someChar);
     } while (( someChar = getchar()) != EOF);
   
     return EXIT_SUCCESS;
   }
   ```

   - The input is coming from standard in and printing to standard out
   - The input is coming from standard error and printing to standard out
   - The input is coming from positional parameters and writing to a file
   - The input is being read directly from a file with a file pointer and printing to standard out.

5. Which of the following code snippets will read from a file and print to standard out (assuming `somefilename.txt` exists): 

   - ```c
     // ....
     FILE * filePointer;
     int character; 
     
     filePointer = fopen("somefilename.txt", "r");
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

6. Which of the following code lines of code will open the file "somefilename.txt" for writing without overwriting any pre-existing data:

   - ```c
     FILE * filePointer = fopen("somefilename.txt", 'a');
     ```

   - ```c
     FILE * filePointer = fopen("somefilename.txt", 'w');
     ```

   - ````
     char* characterString = getc("somefilename.txt");
     ```

   - ```c
     putc("somefilename.txt", 'a');
     ```

     

7. Given the following code, what is the output?
   `options.c`

   ```c
   #include <stdio.h>
   #include <stdlib.h>
   #include <unistd.h>
   
   int main(int argc, char** argv){
     int option;
     while ( (option = getopt(argc, argv, "bw:c:")) != -1) {
       switch(option) {
         case 'b':
                   printf("Cool! ");
           break;
         case 'w':
           printf("%s ", optarg);
           break;
         case 'c':
           printf("%d ", atoi(optarg));
           break;
         default:
           printf("Bad options! ");
           break;
       }
     }
   
     printf("Hello World!\n");
   }
   ```

   ```bash
   gcc options.c -o options
   ./options  -bw beans -c 23
   ```

   

   

   - 
     
     ```bash
   Cool! beans 23 Hello World!
     ```
     
   - ```bash
     Cool!
     beans
     23
     Hello World!
     ```

   - ```bash
     Bad options! Hello World!
     ```

   - ```bash
     Cool!
     Hello World!
     ```

     

8. Given the following code is executing, at line 11 what would the call stack look like (ignoring "address" values for now).

   ```c
   #include <stdio.h>
   
   void function2() {
     int d = 20; 
   }
   
   void function1() {
     int a = 10; 
     function2();
   
      a=500;
   }
   
   int main() {
   	int a = 42; 
     char b = 'B';
     double c = 6.28; 
   
     function1(); 
     
   	return 0;
   }
   ```

   

   - 
     
     | Frame     | Symbol          | Value   |
     | --------- | --------------- | ------- |
     | function1 | a               | 500     |
     | function1 | Return location | line 19 |
     | main      | c               | 3.14    |
   | main      | b               | f       |
     | main      | a               | 23      |
     
     | Frame     | Symbol          | Value   |
     | --------- | --------------- | ------- |
     | function2 | d               | 20      |
     | function2 | Return Location | line 9  |
     | function1 | a               | 500     |
     | function1 | Return location | line 19 |
     | main      | c               | 3.14    |
   | main      | b               | f       |
     | main      | a               | 23      |
     
     | Frame     | Symbol          | Value   |
     | --------- | --------------- | ------- |
     | function1 | a               | 10      |
     | function1 | Return location | line 19 |
     | main      | c               | 3.14    |
   | main      | b               | f       |
     | main      | a               | 23      |
     
     | Frame | Symbol | Value |
     | ----- | ------ | ----- |
     | main  | c      | 3.14  |
     | main  | b      | f     |
     | main  | a      | 23    |

9. Given the following code is executing, at line 4 what would the call stack look like (ignoring "address" values for now). 

   ```c
   #include <stdio.h>
   
   void function2(int b, int c) {
     int d = b + c; 
   }
   
   void function1() {
     int a = 10; 
     function2(a, 25);
   
      a=500;
   }
   
   int main() {
   	int a = 42; 
     char b = 'B';
     double c = 6.28; 
   
     function1(); 
     
   	return 0;
   }
   ```

   -
   
   | Frame     | Symbol          | Value   |
   | --------- | --------------- | ------- |
   | function2 | d               | 35      |
   | function2 | c               | 25      |
   | function2 | b               | 10      |
   | function2 | Return Location | line 9  |
   | function1 | a               | 500     |
   | function1 | Return location | line 19 |
   | main      | c               | 3.14    |
   | main      | b               | f       |
| main      | a               | 23      |
   
   | Frame     | Symbol          | Value   |
   | --------- | --------------- | ------- |
   | function2 | d               | 35      |
   | function1 | a               | 500     |
   | function1 | Return location | line 19 |
   | main      | c               | 3.14    |
   | main      | b               | f       |
   | main      | a               | 23      |
   
   | Frame     | Symbol          | Value   |
   | --------- | --------------- | ------- |
   | function1 | a               | 10      |
   | function1 | Return location | line 19 |
   | main      | c               | 3.14    |
   | main      | b               | f       |
   | main      | a               | 23      |
   
   | Frame | Symbol | Value |
   | ----- | ------ | ----- |
   | main  | c      | 3.14  |
   | main  | b      | f     |
   | main  | a      | 23    |



10. Given the following code is executing, at line 5 what would the call stack look like:  

   ```c
   #include <stdio.h>
   
   int function2(int b, int c) {
     int d = b + c; 
     return d; 
   }
   
   void function1() {
     int a = 10; 
     a=function2();
   }
   
   int main() {
   	int a = 42; 
     char b = 'B';
     double c = 6.28; 
   
     function1(); 
     
   	return 0;
   }
   ```
   
   

| Frame     | Symbol          | Value   | Addrress |
| --------- | --------------- | ------- | -------- |
| function2 | d               | 35      | 140      |
| function2 | c               | 25      | 135      |
| function2 | b               | 10      | 130      |
| function2 | Value Address   | 120     | 127      |
| function2 | Return Location | line 9  | 124      |
| function1 | a               | 500     | 120      |
| function1 | Return location | line 19 | 115      |
| main      | c               | 3.14    | 107      |
| main      | b               | f       | 103      |
| main      | a               | 23      | 100      |

| Frame     | Symbol          | Value   | Address |
| --------- | --------------- | ------- | ------- |
| function2 | d               | 35      | 124     |
| function1 | a               | 500     | 120     |
| function1 | Return location | line 19 | 115     |
| main      | c               | 3.14    | 107     |
| main      | b               | f       | 103     |
| main      | a               | 23      | 100     |

| Frame     | Symbol          | Value   | Address |
| --------- | --------------- | ------- | ------- |
| function1 | a               | 10      | 129     |
| function1 | Return location | line 19 | 115     |
| main      | c               | 3.14    | 107     |
| main      | b               | f       | 104     |
| main      | a               | 23      | 100     |

| Frame | Symbol | Value | Address |
| ----- | ------ | ----- | ------- |
| main  | c      | 3.14  | 150     |
| main  | b      | f     | 129     |
| main  | a      | 23    | 100     |

