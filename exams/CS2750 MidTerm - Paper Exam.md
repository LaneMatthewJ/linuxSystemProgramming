# CS2750 MidTerm

## Name: 

#### True/False 1 point each (10 Questions)

1. True / False  If a user has no execute permissions for a particular directory, they will not be able to access the files within the directory or any files in any subdirectories.   
2. True / False  The `tr` command is used for enforcing line width within a file.  
3. True / False  The `|` operator redirects a program's standard output to another program's standard input   
4. True / False  The `pwd` command updates a the user's password when run 
5. True / False. The `fgrep` command is used for specifically searching files, whereas the `egrep` is used for searching through I/O device data. 
6. True / False The `i-list` is a list of all input/output devices connected to the system
7. True / False By default, all variables in bash are treated as strings.  
8. True / False `..` refers to a directory's parent directory.  
9. True / False.  All positional parameters can be accessed by using `$#`
10. True / False  `tar` combines, compresses, and decompresses files by differing compression algorithms depending on the argument provided. 



#### Multiple Choice 4 points each (10 questions)

1. Given the a directory with the files:

   ```
   file_1  file_2  file_3  file_a  file_b  file_c
   ```

   Which of the following commands will list only: `file_1`, `file_2`, `file_a`, `file_b`: 

   - `ls file[0-9]`
   - `ls file[ab3]`
   - `ls file_[12ab]` 
   - `ls file_*`

2. Which of the following code snippets will result in the output: 

   `Neato`
   `Mosquito`

   ```bash
   #!/bin/bash
   
   someString="Neato,Mosquito"
   
   #### CODE SNIPPET GOES HERE
   
   for something in $someList
   do
   	echo $something
   done
   ```

   - ```bash
     IFS='|'
     read -ra someList <<< $someString
     ```

   - ```bash
     IFS=','
     read -ra someList <<< "$someString"
     ```

   - ```bash
     someList=$(split someString)
     ```
   
   - ```bash
  someList=$(split someString ',')
     ```
   
     

3. Which of the following commands will run the shell script `takeforever.sh` in the background?

   - `./takeforever.sh &` 
   - `./takeforever.sh`
   - `./takeforever.sh ^`
   - `./takeforever.sh $`

4. Given that the most recent command in the shells is `ls -la someDirectory`, which of the following commands would change and update the command to be `ls -la otherDirectory`

   - `$some!other`
   - `^some^other` 
   - `[some]other`
   - `some!other`

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

   Which of the following commands will sort the file by course title? 

   - `sort -k2 -t, faculty_summer_2020.csv`
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

   Which of the following commands will update the the email `mjlny2@umsl.edu` to `mjlane@umsl.edu`? 

   - `sed '/mjlny2/d' faculty_summer_2020.csv`
   - `sed '/mjlny2/mjlane/G' faculty_summer_2020.csv`
   - `sed 's/mjlane/d' faculty_summer_2020.csv`
   - `sed 's/mjlny2/mjlane/' faculty_summer_2020.csv` 

7. Given the file: `faculty_summer_2020.csv`

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

   Which of the following `grep` commands will retrieve only users with phone numbers in the following data:

   - `grep [0-9][0-9][0-9]-[0-9][0-9][0-9][0-9] faculty_summer_2020.csv`
   - `grep [0-9]*  faculty_summer_2020.csv`
   - `grep (0-9)* faculty_summer_2020.csv`
   - `grep {0-9}*3-{0-9}*4 faculty_summer_2020.csv`

8. Given the code: 

   ```bash
   #!/bin/bash
   
   continue="no"
   count=1
   ############# CODE HERE #########
   do
      if [[ count -ge "7" ]]
      then
         $continue="yes"
      fi
   
      echo Hello $count
      $((count++))
   done
   
   echo The program is over
   ```

   Which of the following lines of code is required at line 5 in order to have the output:

   > The program is over

   - `until [[ $continue = "no" ]]` 
   - `while [[ $continue = "no" ]]` 
   - `for [[ i=0; i < $count; i++ ]]`
   - `for (( i=0; i < count; i++))`

9. Which of the following commands will find all text files, and remove read and write permissions for all users? 

   - `find . -name '*.txt' < chmod 700 {}` 
   - ` find . -name '*.txt' | chmod 700`
   - `find . -name '*.txt' -exec chmod a-rw {} \; ` 
   - `find *.txt`

10. Given a file, `twoHundredLines.txt` that is 200 lines long, which of the following commands would you need to use to read lines 75 through 125?

   - `head -n 125 twoHundredLines.txt | tail -n 50`

   - `head -n 75 twoHundredLines.txt | tail -n 125`
   - `head -n 125 twoHundredLines.txt | tail -n 75`

   - `head -n 50 twoHundredLines.txt | tail -n 50`

#### Short Answer 5 points each (8 questions) (be sure to read the questions carefully)

1. List the directories and files created from the following command: 

   ```bash
   mkdir someDirectory_{a,b} && touch someDirectory_{a,b}/{notes.md,assignments.md,anotherFile.c}
   ```

   ```bash

   

   

   

   
   
   
   
   
   
   
   
   
   
   
   
   
   ```
   
   
   
2. Write a short bash script that takes in any number of command line arguments, and changes all input to **upper** case.

   ```
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   ```

3. Write a short bash script that captures SIGKILL and prints "Process cannot be killed" to the console. 

   ````
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   ````

4. Write a grep command that will search history for all previous commands that used an `exec` and redirect the output to a file called `execs.txt`

   ```bash
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   ```

   

5. Write a command or script that displays only files that have greater than 1000 bytes

   ```bash
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   ```

6. Write a sed command that changes all pipe delimited data of a file `pipes.csv` to tilde delimited data, and save it to a file `tildelimited.csv`

   ```bash
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   ```

7. Write a short bash script that takes in 2 numbers, compares them, and returns whether or not the first number is greater, less than, or equal to the second number. 

   ```bash
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   ```

8. Write a sequence of commands that will execute a command in the background, but then immediately bring it to the foreground.

   ```bash
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   ```

   

#### Long Answer 10 pts

1. Write a bash script that prompts a user with a menu of choices: 

   1. Get the total number of shell files from the current directory
   2. Get the total size of all the shell files from the current directory
   3. Get the total number of empty files in the system from the current directory

   Each option must be its own specific function. 

   ```bash
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   ```

   