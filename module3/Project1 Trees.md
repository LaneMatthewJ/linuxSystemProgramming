# Trees 

In many command line interfaces, there is a command called `tree` that either already exists of you can download via a package manager. Delmar doesn't let us do that, unfortunately, so we'll have to build our own. 

For this project, your goal is to create a command line tool that takes in a directory, and prints all of its subdirectories in a formatted fashion. For example, suppose I pass in a directory with its own subdirectories for a project: 

```
example-app
|-- pom.xml
|-- src
|   |-- main
|   |   `-- java
|   |       `-- main
|   |           |-- App.java
|   |           `-- DoMath.java
|   `-- test
|       `-- java
|           `-- main
|               |-- AppTest.java
|               `-- DoMathTest.java
`-- target
    |-- classes
    |   |-- DoMath.class
    |   `-- main
    |       `-- App.class
    |-- generated-sources
    |   `-- annotations
    |-- generated-test-sources
    |   `-- test-annotations
    |-- maven-status
    |   `-- maven-compiler-plugin
    |       |-- compile
    |       |   `-- default-compile
    |       |       |-- createdFiles.lst
    |       |       `-- inputFiles.lst
    |       `-- testCompile
    |           `-- default-testCompile
    |               |-- createdFiles.lst
    |               `-- inputFiles.lst
    |-- surefire-reports
    |   |-- DoMathTest.txt
    |   |-- TEST-DoMathTest.xml
    |   |-- TEST-main.AppTest.xml
    |   `-- main.AppTest.txt
    `-- test-classes
        |-- DoMathTest.class
        `-- main
            `-- AppTest.class
```



Your application should be able to: 

- Determine the filetype of what is passed in, and throw an error / exit if not a directory. 
- Print a tree of the file hierarchy of the supplied directory's subdirectories and files. 

**Bonus points**: Colorize your output to distinguish between ordinary files and directories. 



#### Where to start: 

In our notes, we've created a number of applications that extract information from grep and sed, split strings to act as arrays, and deal with file inputs. 

Start by drawing out what it is you think that the program should do. 

Try doing the program in chunks. Don't attempt to do everything in one sitting. 



#### How to Submit

Submit a copy of your bash script's code via canvas. For now, just copy paste the code directly out of vim or nano (or use cat and print the code to the command line). 