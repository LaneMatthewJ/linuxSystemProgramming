# Project 2

In a learning environment, it's not uncommon to wind up crowded directories filled with a number of files for testing, empty files, and even empty directories. In this project, it is your task to create a command line interface that will prompt a user to see if they would like to: 

1. Search and remove all empty files and directories within the working directory. 
2. Provide a series of filenames to move into their own directory (also provided by the user)
3. Provide a series of filenames to be combined via tar, along with a choice of what method of compression the user would like to use. 
4. Navigate to another directory
5. Exit the program

If a user provides a file or directory name that does not exist, prompt the user with an error message and reprompt the user for the proper file names. 

**Bonus: ** Capture SIGINT and call a function to say goodbye to the user. 