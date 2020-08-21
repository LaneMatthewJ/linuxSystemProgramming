# Module 1 Quiz Questions



- Which of the following will retrieve the last argument of the most recent command

  - `!$`  *
  - `!*`
  - `!^`
  - `!!`

- Which of the following will alias `printUser` with `echo $USER`: 

  - `alias printUser="echo $USER"` *
  - `alias printUser = "echo $USER"`
  - `alias printUser=echo $USER`
  - `alias printUser=echo "$USER"`

- Which of the following commands will **create** two separate directories, `dir_a` and `dir_b`, each with their own files `notes.md` and `assignments.md`: 

  - `mkdir dir_{a,b} && touch dir_{a,b}/{notes.md,assignments.md}` *
  - `mkdir dir_{a,b} || touch dir_{a,b}/{notes.md,assignments.md}`
  - `mkdir dir_{a,b} | touch dir_{a,b}/{notes.md,assignments.md}`
  - `touch dir_{a,b}/{notes.md,assignments.md}`

- Given the a directory with the files:

  ```
  file_1  file_2  file_3  file_a  file_b  file_c
  ```

  Which of the following commands will list only: `file_1`, `file_2`, `file_a`, `file_b`: 

  - `ls file_[12ab]`*
  - `ls file[0-9]`
  - `ls file[ab]`
  - `ls file_*`

- What affect will `chmod 070` have on a file: 

  - u: `_ _ _`  g: `r w x` o: `_ _ _` * 
  - u: `r w x`  g: `_ _ _` o: `r w x`
  - u: `_ _ x`  g: `_ _ x` o: `_ _ x`
  - u: `_ _ _`  g: `r w _` o: `_ _ _`

- Which of the following commands will write the output of the `history`  command to a file and overwrite its contents?: 

  - `history > historyFile.txt`
  - `history < historyFile.txt`
  - `history | historyFile.txt`
  - `history >> historyFile.txt`

- Given the output from `jobs`

  ```bash
  [1]-  Stopped                 ./failforever.sh
  [2]   Running                 ./takeforever.sh &
  [3]+  Stopped                 ./takeforever.sh
  ```

  Which of the following commands will bring `failforever.sh` into the foreground? 

  - `fg %-`
  - `fg -`
  - `fg %+`
  - `fg 2`

- Which of the following commands will run the shell script `takeforever.sh` in the background?

  - `./takeforever.sh &`
  - `./takeforever.sh`
  - `./takeforever.sh ^`
  - `./takeforever.sh $`

- What do the `.` and `..` refer to in a directory: 

  - They are references to the directory itself and its parent directory
  - They are shorthands to execute files
  - They are hidden files that contain data about the directory
  - They are executable files

- Which of the following best describes the Linux Kernel: 

  - Deals with low level operations on the system, such as scheduling , memory management, hardware interfacing, etc. 
  - Creates graphical user interfaces for a rich user experience.
  - Accepts text input from a CLI and runs the given commands.
  - Connects programs and systems through ssh