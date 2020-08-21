# Quiz 7

1. What is the output of the following code? 

   ```c
   #include <stdio.h>
   
   int main(int argc, char** argv){
   	int x = 23; 
     int y = 72; 
     
   	if (x > y);
   	{
   		printf("X is greater than Y");
   	}
     
     printf("End of program!"); 
   }
   ```

   - ```bash
     X is greater than Y
     End of program
     ```

   - ```bash
     End of program
     ```

   - Nothing. The program will fail to compile

   - ```bash
     X is greater than Y
     ```

2. True / False: A program is guaranteed to crash if an index on an array reads out of bounds: 

   - True
   - **False**

3. Which of the following pieces of code **DOES NOT** act as a test that tests whether or not isGreater works: 

   ```c
   #include <stdio.h>
   #include <stdlib.h>
   
   int isGreaterThan(int a, int b){
     return a > b;
   }
   
   void tests() {
     int num1 = 4;
     int num2 = 6;
   	
     isGreaterThan(num1, num2); 
   	exit(1); 
   }
   
   int main(int argc, char** argv){
     	tests(); 
   }
   ```

   

   ```c
   #include <stdio.h>
   #include <stdlib.h>
   
   int isGreaterThan(int a, int b){
     return a > b;
   }
   
   void tests() {
     int num1 = 4;
     int num2 = 6;
     int expectedOutput = 0; 
     int actualOutput = isGreaterThan(num1, num2);
     
     if (expectedOutput != actualOutput) exit(1); 
   }
   
   int main(int argc, char** argv){
     	tests(); 
   }
   ```

   ```c
   #include <stdio.h>
   #include <stdlib.h>
   
   int isGreaterThan(int a, int b){
     return a > b;
   }
   
   void tests() {
     int num1 = 4;
     int num2 = 6;
   
     if (isGreaterThan(num2, num1) != 1){
       exit(1); 
     }
    
   }
   
   int main(int argc, char** argv){
     	tests(); 
   }
   ```

   ```c
   #include <stdio.h>
   #include <stdlib.h>
   
   int isGreaterThan(int a, int b){
     return a > b;
   }
   
   void tests() {
     if(isGreaterThan(0,1) == 0) {
   		exit(1);     
     } 
   }
   
   int main(int argc, char** argv){
     	tests(); 
   }
   ```

   

4. GDB is a tool for: 

   - Debugging code by allowing the user to step through each line, or set up break points for the user to analyze the variables and stack. 
   - A command line tool used for compiling object files. 
   - A command line tool used for linking files together.
   - Source control to ensure that the user can accurately commit, tag, and check out specific versions of the code to ensure code integrity. 

5. In the following code, suppose we used the debugger to stop at like X, what variables are being referred to within that code block (i.e. point to which line number they were declared)? 

   ```c
   #include <stdio.h>
   #include <stdlib.h>
   
   int main(int argc, char** argv){
     int a = 5;
     int b = 10;
     int c = 23;
   
     if (a < b){
       int b = 500;
       int c = 15;
       int i;
       
       for (i = 0; i < 10; i++ ){
         int c = 42;
   
         if( i > 8 ) {
           printf("a:%d b:%d c:%d i:%d", a, b, c, i );
         }
       }
     }
   
     return EXIT_SUCCESS;
   }
   ```

   

   - 

     ```bash
     a:5 b:500 c:42 i:9
     ```

   - ```bash
     a:5 b:10 c:23 i:9
     ```

   - ```bash
     a:5 b:500 c:15 i:9
     ```

   - ```bash
     a:5 b:10 c:42 i:9
     ```

6. What is the output of the following code: 
   `reference.c`

   ```c
   #include <stdio.h>
   #include <stdlib.h>
   
   int main(int argc, char** argv) {
     int a = 23;
     int * b = & a;
   
     * b = a + 1;
   
     printf("%d", a);
   
     return EXIT_SUCCESS;
   }
   ```

   

   - 

     ```bash
     24
     ```

   - ```bash
     23
     ```

   - ```bash
     The address of `a`. 
     ```

   - ```bash
     The address of `a`, incremented by 1. 
     ```

7. What is the output of the following file: 
   `references.c`

   ```c
   #include <stdio.h>
   #include <stdlib.h>
   
   int someFunction(int c, int * d) {
   	c = 200; 
     * d = 400;
   }
   
   int main(int argc, char** argv) {
     int a = 23;
     int b = 42;
   
   	someFunction(a, & b);
     
     printf("a: %d b: %d\n ", a, b);
   
     return EXIT_SUCCESS;
   }
   ```

   

   

   - 

     ```bash
     a: 23 b: 400
     ```

   - ```bash
     a: 23 b: 42
     ```

   - ```bash
     a: 200 b: 400
     ```

   - ```bash
     a: 200 b: 42
     ```

   

   7. What is the output of the following code? 
      `arrayFunc.c`

      ```c
      #include <stdio.h>
      #include <stdlib.h>
      
      
      int seedArr( int size, int* arr) {
      	int i;
        for (i=0; i < size;i++) {
          arr[i] = i; 
        }
      }
      
      int printArr( int size, int* arr) {
      	int i;
        for (i=0; i < size;i++) {
          printf("%d ", arr[i]); 
        }
        printf("\n");
      }
      
      int main(int argc, char** argv) {
      	const int ARR_SIZE = 5;
        int arr [ARR_SIZE]; 
        
       	int i;
        for (i=0; i < ARR_SIZE;i++) {
          arr[i] = 0; 
        }
        
        printArr(ARR_SIZE, arr); 
        seedArr(ARR_SIZE, arr); 
        printArr(ARR_SIZE, arr); 
      
        return EXIT_SUCCESS; 
      }
      ```

      

      - 

        ```bash
        0 0 0 0 0
        0 1 2 3 4
        ```

      - ```bash
        0 0 0 0 0
        0 0 0 0 0
        ```

      - ```bash
        0 1 2 3 4
        0 1 2 3 4
        ```

      - ```bash
        0 1 2 3 4
        0 0 0 0 0
        ```

   8. What is the output of the following code? 

      ```c
      #include <stdio.h>
      #include <stdlib.h>
      
      int main(int argc, char** argv) {
        const int ARR_SIZE = 5;
        int arr [ARR_SIZE];
        int * arrPointer = arr;
      
        int i;
        for (i=0; i < ARR_SIZE;i++) {
          arr[i] = 0;
        }
      
        arrPointer++;
        arrPointer++;
      
        * arrPointer = 7;
      
        for (i=0; i < ARR_SIZE;i++) {
          printf("%d ", arr[i]);
        }
      
        printf("\n");
      
        return EXIT_SUCCESS;
      }
      ```

      

      - 

        ```
        0 0 7 0 0
        ```

      - ```bash
        0 0 0 0 0
        ```

      - ```bash
        0 0 0 7 0
        ```

      - ```bash
        0 7 0 0 0 
        ```

        

   9. True / False When breaking a project up into multiple files, you only need to compile the main file, and don't need to include all files and headers in the compile statement: 

      - **True**
      - False

   10. In a Makefile if a target's dependencies have not changed, the target will be: 

       - Ignored until any changes are made
       - Recompiled
       - Removed
       - Deleted

   