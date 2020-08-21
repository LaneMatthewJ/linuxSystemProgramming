

# CS2750 MidTerm

## Name: 

#### True/False 1 point each (10 Questions)

1. True / False  If a user has no read permissions for a particular directory, they will not be able to access the files within the directory or any files in any subdirectories.   
2. True / False  The `tr` command is used for enforcing line width within a file.  
3. True / False  The `|` operator redirects a program's standard output to overwrite the contents of a file. 
4. True / False  The `pwd` command prints the path to the working directory. 
5. True / False. The commands `fgrep` and `egrep` are both accessible as flags from `grep`. 
6. True / False The `i-node` is a list of mounted i/o devices.
7. True / False It is impossible to assign a value to a bash variable outside of a bash script.   
8. True / False `.` refers to a directory's parent directory.  
9. True / False.  All positional parameters can be accessed by using `$@`
10. True / False  `tar` allows for a user to remotely transfer data to and from a remote server. 



#### Multiple Choice 4 points each (10 questions)

1. Given the a directory with the files:

   ```
   file_1  file_2  file_3  file_a  file_b  file_c
   ```

   Which of the following commands will list only: `file_3`, `file_a`, `file_b`: 

   - `ls file_[0-9]`
   - `ls file_[ab3]`
   - `ls file_[12ab]` 
   - `ls file_*`

2. Which of the following code snippets will result in the output: 

   `Neato`
   `Mosquito`

   ```bash
   #!/bin/bash
   
   someString="Neato|Mosquito"
   
   #### CODE SNIPPET GOES HERE
   
   for something in $someList
   do
   	echo $something
   done
   ```

   - ```bash
     IFS='|'
     read -ra someList <<< "$someString"
     ```

   - ```bash
     someList=$(split someString)
     ```
   
- ```bash
    someList=$(split someString ',')
     ```
   
   - ```bash
      IFS=','
      read -ra someList <<< "$someString"
      ```
   
3. Which of the following commands will take the shell script `takeforever.sh` from the background into the foreground?

   ```bash
   ./takeforever.sh &
   [1] 15828
   ```

   

   - `./takeforever.sh &`
   - `fg takeforever.sh`
   - `./teakforever.sh`
   - `fg 1`

4. Given that the most recent command in the shells is `ls -la cs2750`, which of the following commands would change and update the command to be `ls -la cs3010`

   - `$2750!3010`
   - `^cs3010^cs2750` 
   - `[2750]3010`
   - `^2750^3010`

5. Given the file: `faculty_summer_2020.csv`

   ```
   firstName,	lastName,	email,	phone,	currentClass,	className
   Shawna,	Climer,	climersh@umsl.edu,	,	1250,	Introduction to Computing
   Fadi,	Wedyan,	wedyanf@umsl.edu,	 ,	1250,	Introduction to Computing
   Nazire,	Koc,	kocn@umsl.edu,	314-516-6356,	2250,	Programming andDatastructures
   Steve,	Riegerix,	riegerixs@umsl.edu,	,	2261,	Object Oriented Programming
   Ankit, 	Chaudhary,	chaudharya@umsl.edu,	314-516-4984,	2700,	Computer Organization and Hardware
   Matthew,	Lane,	mjlny2@umsl.edu,	314-282-7563,	2750,	System Programming and Tools
   Steve,	Reigerix,	riegerixs@umsl.edu,	,	3010,	Web Programming
   Gregory,	Hommert,	gmhz7b@umsl.edu,	,	4220,	Introduction to iOS Programming and Apps
   Galina,	Piatnitskaia,	piatnitskaiag@umsl.edu,	314-516-5239,	4250,	Programming Languages
   Mark,	Hauschild,	hauschildm@umsl.edu,	314-516-6426,	4732,	Introduction to Cryptography for Computer Security
   ```

   Which of the following commands will sort the file by course number? 

   - `sort -k5 -t, faculty_summer_2020.csv`
   - `sort -k6 -t, faculty_summer_2020.csv`
   - `sort -t, faculty_summer_ssoid_2020.csv`
   - `sort -k1 faculty_summer_ssoid_2020.csv`

6. Given the file: `faculty_summer_2020.csv`

   ```
   firstName,	lastName,	email,	phone,	currentClass,	className
   Shawna,	Climer,	climersh@umsl.edu,	,	1250,	Introduction to Computing
   Fadi,	Wedyan,	wedyanf@umsl.edu,	 ,	1250,	Introduction to Computing
   Nazire,	Koc,	kocn@umsl.edu,	314-516-6356,	2250,	Programming andDatastructures
   Steve,	Riegerix,	riegerixs@umsl.edu,	,	2261,	Object Oriented Programming
   Ankit, 	Chaudhary,	chaudharya@umsl.edu,	314-516-4984,	2700,	Computer Organization and Hardware
   Matthew,	Lane,	mjlny2@umsl.edu,	314-282-7563,	2750,	System Programming and Tools
   Steve,	Reigerix,	riegerixs@umsl.edu,	,	3010,	Web Programming
   Gregory,	Hommert,	gmhz7b@umsl.edu,	,	4220,	Introduction to iOS Programming and Apps
   Galina,	Piatnitskaia,	piatnitskaiag@umsl.edu,	314-516-5239,	4250,	Programming Languages
   Mark,	Hauschild,	hauschildm@umsl.edu,	314-516-6426,	4732,	Introduction to Cryptography for Computer Security
   ```

   Which of the following commands will update the the field `currentClass` to `courseNumber`? 

   - `sed '/currentClass/d' faculty_summer_2020.csv`
   - `sed '/currentClass/courseNumber/G' faculty_summer_2020.csv`
   - `sed 's/currentClass/d' faculty_summer_2020.csv`
   - `sed 's/currentClass/courseNumber/' faculty_summer_2020.csv` 

7. Given the file: `faculty_summer_2020.csv`

   ```
   firstName,	lastName,	email,	phone,	currentClass,	className
   Shawna,	Climer,	climersh@umsl.edu,	,	1250,	Introduction to Computing
   Fadi,	Wedyan,	wedyanf@umsl.edu,	 ,	1250,	Introduction to Computing
   Nazire,	Koc,	kocn@umsl.edu,	314-516-6356,	2250,	Programming andDatastructures
   Steve,	Riegerix,	riegerixs@umsl.edu,	,	2261,	Object Oriented Programming
   Ankit, 	Chaudhary,	chaudharya@umsl.edu,	314-516-4984,	2700,	Computer Organization and Hardware
   Matthew,	Lane,	mjlny@umsl.edu,	314-282-7563,	2750,	System Programming and Tools
   Steve,	Reigerix,	riegerixs@umsl.edu,	,	3010,	Web Programming
   Gregory,	Hommert,	gmhzb@umsl.edu,	,	4220,	Introduction to iOS Programming and Apps
   Galina,	Piatnitskaia,	piatnitskaiag@umsl.edu,	314-516-5239,	4250,	Programming Languages
   Mark,	Hauschild,	hauschildm@umsl.edu,	314-516-6426,	4732,	Introduction to Cryptography for Computer Security
   ```

   Which of the following `grep` commands will retrieve only users with phone numbers in the previous data:

   - `grep [a-z] faculty_summer_2020.csv`
   - `grep [a-z]*@  faculty_summer_2020.csv`
   - `grep (a-z)* faculty_summer_2020.csv`
   - `grep {a-z}*5 faculty_summer_2020.csv`

8. Given the code: 

   ```bash
   #!/bin/bash
   
   continue="no"
   count=1
   ############# CODE HERE #########
   do
      if [[ count -ge "3" ]]
      then
         continue="yes"
      fi
   
      echo Hello $((count++))
      
   done
   
   echo The program is over
   ```

   Which of the following lines of code is required at line 5 in order to have the output:

   > Hello 1
   >
   > Hello 2
   >
   > The program is over

   - `until [[ $continue = "no" ]]` 
   - `while [[ $continue = "no" ]]` 
   - `for [[ i=0; i < $count; i++ ]]`
   - `for (( i=0; i < count; i++))`

9. Which of the following commands will find all shell files, and add read and write permissions for all users? 

   - `find . -name '*.sh' < chmod 700 {}` 
   - `find . -name '*.sh' -exec chmod a+rw {} \; ` 
   - `find . -name '*.txt' -exec chmod a-rw {} \; ` 
   - `find *.txt`

10. Given a file, `twoHundredLines.txt` that is 200 lines long, which of the following commands would you need to use to read lines 100 through 125?

   - `head -n 125 twoHundredLines.txt | tail -n 50`

   - `head -n 75 twoHundredLines.txt | tail -n 125`
   - `head -n 125 twoHundredLines.txt | tail -n 25`

   - `head -n 50 twoHundredLines.txt | tail -n 50`

#### Short Answer 5 points each (8 questions) (be sure to read the questions carefully)

1. List the directories and files created from the following command: 

   ```bash
   mkdir some{Dir,dir}ectory_{a,b} && touch some{Dir,dir}ectory_a/file1_{one,two}
   ```

   ```bash

   

   

   

   
   
   
   
   
   
   
   
   
   
   
   
   
   ```
   
   
   
2. Write a short bash script that reads input from standard in, and changes all input to **lower** case.

   ```
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   ```

3. Write a short bash script that throws an error "Error, undefined variable" if a variable is undefined. 

   ````
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   ````

4. Write a grep command that will search history for all previous commands that used a substitution script and redirect the output to a file called `substitution.txt`

   ```bash
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   ```

   

5. Write a command or script that displays only files that have less  than 400 bytes

   ```bash
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   ```

6. Write a sed command that changes all tilde delimited data of a file `tildes.csv` to tilde delimited data, and save it to a file `pipes.csv`

   ```bash
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   ```

7. Write a short bash script that takes in command line arguments, compares them, and returns whether or not the first argument string is greater, less than, or equal to the second argument string. 

   ```bash
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   ```

8. Write a brief script that will loop retrieve only directories in the working directory, and then store those directories into a single variable

   ```bash
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   ```

   

#### Long Answer 10 pts

1. Write a bash script that prompts a user with a menu of choices: 

   1. Get the total number of files from the current directory
   2. Get the total size of all the c files from the current directory
   3. Get the total number of empty files in the system from the current directory

   Each option must be its own specific function. 

   ```bash
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   ```

   