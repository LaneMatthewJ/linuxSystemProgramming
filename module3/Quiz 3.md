Quiz 3

1. What is the output of the following command: 
   `someFile.sh`

   ```bash
   #!/bin/bash
   
   for argument in "$*"
   do
   	echo argument is: $argument      	
   done
   ```

   ```bash
   ./someFile here are "positional parameters"
   ```

   

   - ```
     argument is: here are positional parameters
     ```

   - ```
     argument is: here
     argument is: area
     argument is: positional
     argument is: parameters
     ```

   - ```
     argument is: here
     argument is: are
     argument is: positional parameters
     ```

   - ```
     argument is: here are
     argument is: positional parameters
     ```

     

2. What is the output of the following Command: 
   `greaterOrLessThan.sh`

   ```bash
   #!/bin/bash
   
   someNumber=5
   
   if [[ $someNumber > 10 ]]
   then
       echo $someNumber is greater than 10
   else
       echo $someNumber is not greater than 10
   fi
   ```

   ```bash
   ./greaterOrLessThan.sh
   ```

   - ```bash
     5 is greater than 10
     ```

   - ```
     5 is not greater than 10
     ```

   - ```
     someNumber is greater than 10
     ```

   - ```
     someNumber is not greater than 10
     ```

     

3. What is the ouput of the following commands 
   `greaterOrLessThan.sh`

   ```bash
   #!/bin/bash
   
   someNumber=5
   
   if (( $someNumber > 10 ))
   then
       echo $someNumber is greater than 10
   else
       echo $someNumber is not greater than 10
   fi
   ```

      ```bash
   ./greaterOrLessThan.sh
   
   
      ```

      - 
        
        
   ```
        5 is not greater than 10
   ```
   
   - ```
     5 is greater than 10
     ```

      - ```
        someNumber is greater than 10
        ```

      - ```
        someNumber is not greater than 10
        ```

   

4. Which of the following commands will capture an interrupt

   

   ```bash
   #!/bin/bash
   
   trap "echo Interrupt Caught!" SIGINT
   
   ### Some more logic
   ```

   
   

   ```bash
   #!/bin/bash
   
   trap  SIGINT
   
   if [[ trap ]] 
   then 
   	echo Interrupt Caught!
   fi
   
   ### Some more logic
   ```

   

   ```bash
   #!/bin/bash
   
   catch SIGINT "echo Interrupt Caught"
   
   ### Some more logic
   ```

   

   ```bash
   #!/bin/bash
   
   catch SIGINT
   
   if [[ catch ]] 
   then 
   	echo Interrupt Caught!
   fi
   
   ### Some more logic
   ```

   

   

5. What is the output of the following code
   `shiftyUntil.sh`

   ```bash
   #!/bin/bash
   
   inputVariables="$@"
   continue=$1
   
   until [[ $continue = "no" ]]
   do
           echo You input: $continue
   				shift
   				continue=$1
   done
   
   echo You\'re Done!
   ```

   ```
   ./shiftyUntil.sh no ifs ands or buts
   ```

   

   - You're Done! 
   - You input: no
   - You input: no
     You input: no
     You input: no
     .... 
     (infinitely repeating)
   - You input: no
     You input: ifs
     You input: ands
     You input: or
     You input: buts

   

   

   

6. What is the output of the following code: 
   `funcyFile.sh`

   ```bash
   #!/bin/bash
   
   function boringFunc () {
   	echo your func parameters are: $1 and $2
   }
   
   echo your parameters are: $1 and $2 
   
   someFuncWithArgs afterwhile crocodile
   ```

   ```bash
   ./funkyFile later alligator
   ```

   

   - your parameters are: later alligator
     your func parameters are: afterwhile  crocodile
   - your parameters are: later alligator
     your func parameters are: later alligator
   - your func parameters are: afterwhile  crocodile
     your parameters are: later alligator
   - your func parameters are: later alligator
     your parameters are: later alligator

   

7. Which of the following functions return only the value "cool"

   ```bash
   #!/bin/bash
   function coolFunc () {
   	echo cool
   }
   
   var=$(coolFunc)
   ```

   

   

   ```bash
   #!/bin/bash
   function coolFunc () {
   	return "cool"
   }
   
   var=coolFunc
   ```

   

   

   ```bash
   #!/bin/bash
   function coolFunc () {
   	echo Its so cold, its
   	echo cool
   }
   
   var=coolFunc
   ```

   

   

   ```bash
   #!/bin/bash
   function coolFunc () {
   	return "cool"
   }
   
   var=$?
   ```

   

8. Which of the following code snippets will result in the output: 
   The output is: Hello
   The output is: there

   


   `internalFieldSeparatorEx.sh`

   ```bash
#!/bin/bash

salutation="Hello|There"

#### CODE SNIPPET GOES HERE

for var in $list
do
echo The output is: $var      	
done
   ```

   - 

     

     ```bash
     IFS='|'
     read -ra list <<< "$salutation"
     ```

   - ```bash
     IFS='.'
     read -ra list <<< "$salutation"
     ```

   - ```bash
     list=$(split salutation)
     ```

   - ```bash
     list=$(split salutation '|')
     ```

     

9. What is the output of the following
   `case.sh`

   ```bash
   #!/bin/bash
   
   case $1 in
    [^bBhHyY]ard)
       echo In the first case!
       ;;
     [bB]ard)
       echo In the second!
       ;;
   	*)
   		echo In the third!
       exit
       ;;
   esac
   ```

   ```bash
   ./case.sh yard
   ```

   - In the third!
   - In the first! 
   - In the second! 
   - No output

10. What is the output of the following code: 

    ```bash
    #!/bin/bash
    
    echo Starting the script! 
    ${someVariable:?"What happened!"}
    echo some variable is $someVariable
    echo I can\'t believe that happened
    ```

    - Starting the script!
      ./example.sh: line 4: someVariable: What happened!
    - Starting the script!
      some variable is What happened!
    - Starting the script!
      I can't believe that happened
    - Starting the script! 
      some variable is What happened!
      I can't believe that happened

