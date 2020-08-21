# Quiz 2

1. Given a file, `twoHundredLines.txt` that is 200 lines long, which of the following commands would you need to use to read lines 75 through 125?

   1. `head -n 125 twoHundredLines.txt | tail -n 50`
   2. `head -n 75 twoHundredLines.txt | tail -n 125`
   3. `head -n 125 twoHundredLines.txt | tail -n 75`
   4. `head -n 50 twoHundredLines.txt | tail -n 50`

2. Given a file `oneLine.txt` that has all of its text stored on a single line, which of the following would limit the length of each line by 120 characters without clipping words: 

   1. `fold -w 120 -s oneLine.txt`
   2. `tr [:newline:] 120 oneLine.txt`
   3. `fold -w 120 oneLine.txt`
   4. `tr -w 120 oneLine.txt`

3. Which of the following commands would change a file's characters from `|` to `&` in a file `userList`: 

   1. `tr \| \& < userList.txt`
   2. `tr -d | userList.txt`
   3. `tr | & < userList.txt`
   4. `tr \& \| userList`

4. Which of the following best describes the differences between `grep`, `fgrep`, and `egrep`: 

   1. `fgrep` and `egrep` are aliases for `grep -F` and `grep -E` respectively. 
   2. `grep` is used for searching the command line, `fgrep` searches only files, and `egrep` is used for searching editors
   3. `grep` is used for searching, `fgrep` searches, but can also edit, `egrep` can search, edit, and implement logic
   4. `fgrep` is a recursive search through the filesystem, while `egrep` is used for searching via network calls

   

   Given the following History Text (obtained from the history command): 

   ```bash
   mkdir directory{1,2,3,4}
   cd directory1 && touch file_{a,b,c}
   cd .. 
   cd direcotry2 && touch file_{1,2,3}
   echo Here is some data > file_1
   cd ../directory1
   ls -la
   cd ..
   cd directory3 
   echo This file has data now! > file_{a,b}
   cd ../directory4
   ```

   

5. Which of the following `grep` commands will find the command at line 9? 

   1. `history | grep now!`
   2. `history | grep data`
   3. `history | grep >`
   4. `history | grep echo`

   


   `faculty_summer_2020.csv`

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

   

6. Which of the following `grep` commands will retrieve only users with phone numbers in the following data:

   1. `grep [0-9][0-9][0-9]-[0-9][0-9][0-9][0-9] faculty_summer_2020.csv`
   2. `grep [0-9]*  faculty_summer_2020.csv`
   3. `grep (0-9)* faculty_summer_2020.csv`
   4. `grep {0-9}*3-{0-9}*4 faculty_summer_2020.csv`

7. Which of the following `sed` commands will add a new line only after the email `mjlny2` to the output?

   1. `sed '/mjlny2/G' faculty_summer_2020.csv`
   2. `sed '/mjlny2/d'  faculty_summer_2020.csv`
   3. `sed '/mjlny2/\n'  faculty_summer_2020.csv`
   4. `sed '/mjlny2/' faculty_summer_2020.csv`

8. Which of the following `sed` commands will update the CSV email column to become an SSOid column and save it to a new file? 

   1. `sed 's/email/ssoid/' faculty_summer_2020.csv | sed 's/@umsl.edu//' > faculty_summer_ssoid_2020.csv`
   2. `sed 's/ssoid/email/' faculty_summer_2020.csv | sed 's/@umsl.edu//' > faculty_summer_ssoid_2020.csv`
   3. `sed 's/@umsl.edu//'  < faculty_summer_2020.csv` 
   4. `sed 's/@umsl.edu/ssoid/d' > faculty_summer_ssoid_2020.csv` 

9. Which of the following `sed` commands will delete the line with the username `mjlny2`?

   1. `sed '/mjlny2/d' faculty_summer_2020.csv`
   2. `sed '/mjlny2/G' facultly_summer_2020.csv`
   3. `sed '/[mjlny2]/d' facultly_summer_2020.csv`
   4. `sed '/[^mjlny2]/d' facultly_summer_2020.csv`

10. Which of the following commands will sort the following data by last name?

    1. `sort -k2 -t, facultly_summer_2020.csv`
    2. `sort -k3 -t| facultly_summer_2020.csv`
    3. `sort -t,  facultly_summer_2020.csv`
    4. `sort -k1  facultly_summer_2020.csv`

