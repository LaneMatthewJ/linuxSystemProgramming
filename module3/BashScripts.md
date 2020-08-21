# Bash Scripts

As we've seen so far, a bash script really just seems to be a file with a series of bash commands. Ultimately speaking, any file that is just a series of shell commands is a *shell script*, however, since we're primarily working in bash, we call them *bash scripts*. These scripts are invoked just as any other program (i.e. by providing the shell a full or relative path to the script). Most shells do follow similar, syntax, though, so what works in one shell ought to mostly work in another. 

### 3.1 Running a Bash Script

This was touched on a bit in chapter one, but it's good to go over it again: When you run a script with the **interactive shell** (i.e. the shell you're working in),  you're launching an **invoked shell** that is running the script itself. A great example of this is in the example of a file named `changeDirectoryAndPrint` in your home directory: 

```bash
cd /usr/lib
pwd
```

If you then run the following commands (after having changed execution permissions of the script `changeDirectoryAndPrint`), you'll notice something curious: 

```bash
echo In interactive Shell && pwd && echo running script
```

> In interactive Shell
> /home/mjlny2/2750Materials/module3/ch5
> running script

```bash
./changeDirectoryAndPrint
```

> /usr/lib

```bash
echo Finished with Script && pwd
```

> Finished with Script
> /home/mjlny2/2750Materials/module3/ch5

Granted, in the above examples, your `pwd` output may be different because you're likely in a different directory, however, notice that after we ran the script `changeDirectoryAndPrint` when we then ran `pwd`, our path was still in the original directory of the script itself. What happened is that the shell spins off a sub shell that runs the commands, while the interactive shell sits there waiting for the sub shell to finish its commands. 

To run the commands themselves within the interactive shell, you'll need to use the `source` command: 

```bash
source ./changeDirectoryAndPrint
pwd
```

> /usr/lib



### 5.2 Bash Scripts

Up to now, many of the "bash scripts" that we've seen have been relatively uninterseting. A bash script is really just a file that consists of a series of commands to be run in a sub shell (or a shell, if you source the script). We've been relatively lax about how we've been writing these "bash scripts". When writing a script, it is necessary that you prefix your entire script with: 

```bash
#!/bin/bash
```

By doing so, you ensure that your script is always run by bash, as opposed to any other shell that your terminal might be running. As of now, we've been able to get away with writing our scripts without the prefix because we've specifically been running bash. 

Let's revisit `takesArguments.sh` from chapter 3: 

```bash
#!/bin/bash

echo arg0 $0
echo arg1 $1
echo arg2 $2
echo arg3 $3
echo arg4	$4
```

The script `takesArguments.sh` is nothing too terribly exciting, except it is a great example of *postional parameters*. These parameters refer specifically to the positions they were passed in: 

```bash
./takesArguments.sh firstArg secondArg thirdArg fourthArg
```

> arg0 /home/mjlny2/takesArguments.sh
> arg1 firstArg
> arg2 secondArg
> arg3 thirdArg
> arg4 fourthArg

The first of these arguments, `arg0`, refers entirely to the command itself (by its full name). Naturally, `firstArg` refers to `$1`, `secondArg` to `$2`, and so on. 

**Note: ** to execute bash scripts without referring to the relative or full path, you will need to place them in a directory in the command search path (see chapter 3). 



### 5.3 Shell Script Execution 

There are a number of things to keep in mind as a shell script executes. Each script runs commands separated by new lines (multiple commands can be on the same line if they're delimited by a `;`). Comments, unlike c-style languages, are started with a `#`. 

The general flow of a shell script is: 

1. The shell tokenizes the command and the input (all arguments are assigned *positional parameter* values)
2. Read next command in sequence
   - If no commands next in sequence, **return exit status** (typically 0 for success)
3. Runs next command.
   - If succeeds, return to #2
4. Check if command is build-in: 
   - If command not built in: return to #2
   - If command is built in: **return exit status** (typically non-zero for failure)



As we move throughout the chapter, we may come across the terms:

- Commandlist: commands in a shell script separated by new lines or semicolons
- Wordlist: words delimited by whitespace.



### 5.4 Positional Parameters

In section 5.2, we saw positional parameters, and in section 5.3 we saw that the shell tokenizes the command line input to refer to those positional parameters. The one thing we have not seen out of this is that it is possible to obtain all arguments passed in with either the `*` or `@` symbols. Create a file: `takesArgumentsAgain.sh`: 

```bash
#!/bin/bash

echo arg0 $0
echo arg1 $1
echo arg2 $2
echo arg@ $@
echo arg* $*
```

And make sure to change the mode so that you can execute the file: 

```bash
 ./takesArgumentsAgain.sh one two three four
```

> arg0 ./takesArgumentsAgain.sh
> arg1 one
> arg2 two
> arg@ one two three four
> arg* one two three four

Both the `@` and the `*` act as wild cards so that you can grab all of the arguments. This could come in handy if there were significantly more than 2 or 3 arguments, and you needed an array to be able to work with them all. 



## Treating Bash as a Language:

Up to now, we've been working with bash as if it were just a series of commands. While that is true, however, there are a number of commands that exist within bash that allow us to use loops, conditionals, and more. In this section, we're going to take a look at these and their syntax: 

### Loops: `for`

No language, be it compiled or scripting, would be complete without a loop! The `for` command allows for us to loop over a wordlist (i.e. a series of elements, or words, delimited by whitespace), with the general syntax of: 

```bash
for var in wordlist
do commandlist
done
```

What is happening above is that we are saying: For each element in `wordlist`, execute `commandlist`.  To refer to each individual element within the list, you can use `var`. And for what to do within the `commandlist`, you can simply use as many commands with line breaks or semicolon delimited commands too. 

Let's make this a bit more real by rewriting `takesArguments.sh` to use a loop instead of printing out each element by its *positional parameter*: 

`takesArgumentsLoop.sh`

```bash
#!/bin/bash

for argument in $@
do
	echo  One of our arguments is:
	echo       $argument      
	
done
```

If we then change the mode of `takesArgumentsLoop.sh` and run it: 

```bash
./takesArgumentsLoop.sh I am an argument
```

> One of our arguments is:
> I
> One of our arguments is:
> am
> One of our arguments is:
> an
> One of our arguments is:
> argument
> One of our arguments is:
> list



It may be the case that one day you wish to take in a string with whitespace as a singular argument. What would happen if you attempted that now: 

```bash
./takesArgumentsLoop.sh I am an "argument list"
```

> One of our arguments is:
> I
> One of our arguments is:
> am
> One of our arguments is:
> an
> One of our arguments is:
> argument
> One of our arguments is:
> list



#### Using Strings for Arguments:

**`"$@"`**

Now, here is where some things can get a bit curious with the `$*` and the `$@` variables. If you wrap the variables in quotations

```bash
#!/bin/bash

for argument in "$@"
do
	echo  One of our arguments is:
	echo       $argument      
	
done
```

All we've done differently above is wrap the `$@` in quotation marks. Suppose then we had a string input for a command: 

```bash
./loopWithAt.sh I am an "argument list"
```

> One of our arguments is:
> I
> One of our arguments is:
> am
> One of our arguments is:
> an
> One of our arguments is:
> argument list

By wrapping the `$@` in quotation marks, it then allows for us to treat a quoted value as a singular input. 

**`"$*"`**

What we saw above cannot be said for `$*`. Though they work the same when not quoted, the two variables have different output when inside of quotes: 

```bash
#!/bin/bash

for argument in "$*"
do
	echo  One of our arguments is:
	echo       $argument      
	
done
```

```bash
./loopWithStar.sh I am an "argument list"
```

> One of our arguments is:
> I am an argument list

By using the `$*` option, we don't so much treat our variable at `$4` as its own variable, we instead treat the entire argument list as a singular variable. 

#### C-like Syntax

Bash scripts do allow for us to use c-like syntax. In a file called `clikeLoop.sh` write: 

```bash
#!/bin/bash

for ((i = 0; i < 5; i++))
do
 echo count to $i
done
```

Naturally, this does exactly what we would expect of any for loop: 

```bash
./clikeLoop.sh
```

> count to 0
> count to 1
> count to 2
> count to 3
> count to 4

**Note:** Looping will be further discussed in  sections 11 and 14. 



### 5.6 The `If` Command

Programs could not be anywhere near as robust as they are if it weren't for control flow with if/else commands. The general syntax for the bash if/else construct is: 

```bash
if testExpression
then
	some_commandlist
else
  someOther_commandlist
fi
```

Test expressions will be covered more in the following section, but ultimately follow the general syntax of: 

```bash
[[ a<b ]]
```

Where the condition being tested is written within two square brackets `[[ TEST_CONDITIONS ]]` and return some exit status value. For now, we'll stick to relatively simple tests. Let's write a quick to determine how many directories are in our directory: 

```bash
ls -l | grep ^[d] | wc -l
```

> 18

Now, suppose we wished to write a bash script that would let us know if we ever went over 10 subdirectories within a directory. We could do that by writing a file, `greaterThan10.sh`: 

```bash
#!/bin/bash

directoryCount=$(ls -l | grep ^[d] | wc -l)

if [[ $directoryCount -gt 10 ]]
then
    echo You have more than 10 directories!
else
    echo Not greater than 10
fi
```

Now, if you run this script in a directory with less than 10 directories, you'll wind up with an output: 

> Not greater than 10

However, let's see what happens when we run this in a directory with more than ten directories (and to ensure this, enter the following command): 

```bash
mkdir emptyDirectory{1,2,3,4,5,6,7,8,9,10,11}
./greaterThan10.sh
```

> GREATER THAN 10

What if we wished to be a little more discerning? We could create a script that warns us if we have between 5 and 10 subdirectories, and then flat out yells at us if we have more! To do this, we could nest our if/else statements, however, just like many other languages, we can use the bash equivalent of the `else/if`. 

So, in the following script, we can extract the command so we're not using it more than once, and we can also spice up our output a bit and add some colors: 

```bash
#!/bin/bash

directoryCount=$(ls -l | grep ^[d] | wc -l)
RED_COLORATION='\033[0;31m' #red color
NO_COLORATION='\033[0m'   #no color
ORANGE_COLORATION='\033[0;33m' #orange color

if [[ $directoryCount -gt 10 ]]
then
    printf "${RED_COLORATION}GREATER THAN 10 DIRECTORIES ${NO_COLORATION} Please rethink your subdirectory solutions!\n"
elif [[ $directoryCount -gt  5 ]]
then
    printf "${ORANGE_COLORATION}Warning! You have $directoryCount directories!${NO_COLORATION} You may wish to reconsider this many\n"
else
    echo Not greater than 10
fi
```

One major takeaway for nested conditionals is that immediately after the `elif` and its condition, we have another `then`. 



### 5.8 Shift

You may wish to write a script that works with the positional parameters, but you wish to treat them like a queue. You can shift the positional parameters up in the "queue" by using `shift`: 

`shiftExample.sh`

```bash
#!/bin/bash

echo original values
echo argument0 $0
echo argument1 $1
echo argument2 $2
echo argument3 $3
echo
echo Shifting
shift
echo argument0 $0
echo argument1 $1
echo argument2 $2
echo argument3 $3
echo
echo Shifting
shift
echo argument0 $0
echo argument1 $1
echo argument2 $2
echo argument3 $3
echo
echo Shifting
shift
echo argument0 $0
echo argument1 $1
echo argument2 $2
echo argument3 $3
```

Now, we can see that we're calling up to the third positional parameter. Let's call the shell script with four, just to see what happens: 

```bash
./shiftExample.sh one two three four
```

> original values
> argument0 ./shiftExample.sh
> argument1 one
> argument2 two
> argument3 three
>
> Shifting
> argument0 ./shiftExample.sh
> argument1 two
> argument2 three
> argument3 four
>
> Shifting
> argument0 ./shiftExample.sh
> argument1 three
> argument2 four
> argument3
>
> Shifting
> argument0 ./shiftExample.sh
> argument1 four
> argument2
> argument3

What happened? After every time we print each of the arguments, we shift, dequeuing the value in  argument `$1` , and then shifting all other positional arguments to a new position: `n-1`. 


Or, you can also use a loop as well, though its execution may look a bit more confusing: 

`shiftExample2.sh`

```bash
#!/bin/bash

echo original values

for val in $*
do
  echo \$\* = $*
  echo val = $val
  echo argument0 $0
  echo argument1 $1
  echo argument2 $2
  echo argument3 $3
  echo
  echo Shifting
  shift
done
```

We've got a couple more prints in here to see what's going on, but it's still the same information: 

```bash
./shiftExample2.sh one two three four
```

> original values
> $* = one two three four
> val = one
> argument0 ./shiftExample2.sh
> argument1 one
> argument2 two
> argument3 three
>
> Shifting
> $* = two three four
> val = two
> argument0 ./shiftExample2.sh
> argument1 two
> argument2 three
> argument3 four
>
> Shifting
> $* = three four
> val = three
> argument0 ./shiftExample2.sh
> argument1 three
> argument2 four
> argument3
>
> Shifting
> $* = four
> val = four
> argument0 ./shiftExample2.sh
> argument1 four
> argument2
> argument3
>
> Shifting



### 5.9 Case

The if/else commands let us have conditional statements, but we can also use the `case` command to use pattern matching. The general syntax of `case` is: 

```bash
case (someString) in
matchingPattern) command
	;;
machingPattern2) command2
	;; 
*) command3 #default
esac
```





### Putting it All Together

Suppose we wished, then, to have a shell script that helped us increment the version of a program. Semantic versioning (or semver) is a general convention for software where a piece of software has an a 3 part version number: 

```bash
find --version
```

> find (GNU findutils) 4.5.11
> Copyright (C) 2012 Free Software Foundation, Inc.
> License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>.
> This is free software: you are free to change and redistribute it.
> There is NO WARRANTY, to the extent permitted by law.
>
> Written by Eric B. Decker, James Youngman, and Kevin Dalley.
> Features enabled: D_TYPE O_NOFOLLOW(enabled) LEAF_OPTIMISATION FTS(FTS_CWDFD) CBO(level=2)

The version of `find` is `4.5.11`. Semvers follow the pattern `major.minor.patch`, where typically major versions include breaking changes (like the functionality of inputs change), minor versions (new functionality), and patch versions (bug fixes). 

Let's write a shell script that matches on the type of version bump we'd like, which would then update the version number within a file (i.e. the program we want to increment). First we'll need a very simple bash script to act as our program: 

`versionedProgram.sh`

```bash
#!/bin/bash

VERSION=0.0.0

echo I am a boring program. My version is $VERSION
```

Now, we could bump the version ourselves, however, opening a file, finding the version, and incrementing it is significantly more labor intensive than just typing a command and passing a file name and a type of version bump. So, in the following file, we'll use case to match on the type of version bumping we want to do, and then use `sed` to find the version. Additionally, we'll want to use the `if` command to determine if the input is even valid: 

`versionBump.sh`

```bash
#!/bin/bash
NO_COLORATION='\033[0m'   #no color


versionType=$1
fileName=$2

echo You wish to increment the $versionType version for $fileName

if [ ! -f ./$fileName ]; then
     printf "$fileName ${RED_COLORATION}does not exist.${NO_COLORATION}\n"
     exit
fi



currentVersion=$(sed -n 's/VERSION=//p' $fileName)
echo The current version of $fileName is $currentVersion

case $versionType in
[Mm]ajor)
    echo Major version bump:
    ;;
[Mm]inor)
    echo Minor version bump:
    ;;
[Pp]atch)
    echo Patch version bump:
    ;;
*) 
		printf "${RED_COLORATION}Bad version bump input.${NO_COLORATION}\n"
		echo The possible input values for version type are: "Major" \| "Minor" \| "Patch"
    exit
    ;;
esac

newVersion=$(sed -n 's/VERSION=//p' $fileName)
echo File version is now $newVersion
```

So far, we haven't learned to parse the string so that we can extract each of the elements. Not quite yet. However, we'll come back to this program in not too long once we get to arrays! 

You may also have noticed above that we used a single bracket in our `if` instead of a double bracket like in the `if` section. Double brackets are a bash construction allowing for compound commands, while single brackets are POSIX, allowing for shell built in commands. You can use shell built in commands in the double brackets, so it may be wise just to use double brackets in bash environments all the time. 

### 5.10 While / Until, and User Input

`while` and `until`  loops also exist in bash. While loops operate just the same as other languages, and the  `until` loop works as a `while` loop that's testCondition is the opposite. The test expressions look similar to those of the `if` command. The while loop's general syntax is as: 

```bash
while [[ testCondition ]]
do
	commandlist
done
```

The same syntax works for the `until` loop: 

```bash
until [[ testCondition ]]
do
  commandlist
done
```

Often times, when you write a `while` loop, it's typically to display a menu and to get some amount of user input. Til now, we haven't had any user input other than writing commands directly to the command line and passing in arguments. To retrieve input from the within a script, we'll need to use the `read` command. In the below toy problem, we'll take in some input and manipulate it!

`whileExample.sh`

```bash
#!/bin/bash

name="Some name"
again="yes"

while [[ $again = "yes" ]]
do
        echo What\'s your name?
        read name
        allCaps=$(echo $name | tr [a-z] [A-Z])
        echo Hello $name! If I were to shout your name, it would be: $allCaps

        echo Would you like me to read your name and shout it again? \(yes or no would be sufficient!\)
        read again

done

echo It has been too fun!
```

Above, we're using a while loop, where our condition for continuing the loop is where the variable `again` must equal `"yes"`. First, though, we want to read in a name, just for fun. We prompt the user, read the name with `read` , and store whatever is read into the `name` variable. From there, we translate it with the command expansions, and store it into `allCaps`, where we then print it out again with echo. 

Finally, we prompt the user if they'd like to go through the process again. Any answer that is not yes will stop the loop. 

```bash
./whileExample.sh
```

> What's your name?
>
> Matt
>
> Hello Matt! If I were to shout your name, it would be: MATT
>
> Would you like me to read your name and shout it again? (yes or no would be sufficient!)
>
> no
>
> It has been too fun!

Conversely, were we to use the `until` command: 

`untilExample.sh`

```bash
#!/bin/bash

name="Some name"
again="yes"

until [[ $again = "no" ]]
do
        echo What\'s your name?
        read name
        allCaps=$(echo $name | tr [a-z] [A-Z])
        echo Hello $name! If I were to shout your name, it would be: $allCaps

        echo Would you like me to read your name and shout it again? \(yes or no would be sufficient!\)
        read again

done

echo It has been too fun!
```

Seeing that in action: 

```bash
./untilExample.sh
```

> What's your name?
>
> Matt
>
> Hello Matt! If I were to shout your name, it would be: MATT
>
> Would you like me to read your name and shout it again? (yes or no would be sufficient!)
>
> eh, I dunno
>
> What's your name?
>
> matt...
>
> Hello matt...! If I were to shout your name, it would be: MATT...
>
> Would you like me to read your name and shout it again? (yes or no would be sufficient!)
>
> no
>
> It has been too fun!

 Ultimately speaking, the `while` and `until`  commands do the same thing, but they're just checking for the opposite boolean values. 



### 5.11 Numerical Expressions

Doing math inside of a shell script can confusing. Suppose we had a quick script:

 `badMath.sh`: 

```bash
#!/bin/bash

one=1
two=2

echo one is $one
echo two is $two

three=$one+$two
echo $one + $two is: $three
```

Upon running this script, you'd very likely expect to see: `1 + 2 is: 3`. However, the actual output is: 

```bash
./badMath
```

> one is 1
>
> two is 2
>
> 1 + 2 is: 1+2

We've danced around this so far. Every variable stored in bash is string valued. However, there are a number of times in which you'll need to do arithmetic operations. We saw arithmetic expansions earlier with: 

```bash
echo $(( 1 + 2 ))
```

> 3

But you can also use the `let` command to make your code a bit more readable (without having to use expansions): 

`goodMath.sh`

```bash
#!/bin/bash

one=1
two=2

echo one is $one
echo two is $two

let three=$one+$two
echo $one + $two is: $three
```

By prefixing the assignment of `three` with `let`, we are then telling the shell to do the maths! 



#### Numerical Expressions with Conditionals: 

When looking to use numerical values in conditionals, there are a number of ways to go about this. 

##### Flags

We've seen one above already using flags:  

```bash
#!/bin/bash

directoryCount=$(ls -l | grep ^[d] | wc -l)
RED_COLORATION='\033[0;31m' #red color
NO_COLORATION='\033[0m'   #no color
ORANGE_COLORATION='\033[0;33m' #orange color

if [[ $directoryCount -gt 10 ]]
then
    printf "${RED_COLORATION}GREATER THAN 10 DIRECTORIES ${NO_COLORATION} Please rethink your subdirectory solutions!\n"
elif [[ $directoryCount -gt  5 ]]
then
    printf "${ORANGE_COLORATION}Warning! You have $directoryCount directories!${NO_COLORATION} You may wish to reconsider this many\n"
else
    echo Not greater than 10
fi
```

There are a number of [flags for if](https://www.gnu.org/software/bash/manual/html_node/Bash-Conditional-Expressions.html). By using the correct flags, you can specify that the values you're comparing are integers: 

- `-eq`:  is equal to
- `-ne`:  is not equal to
- `-lt`:  is less than 
- `-le`:  is less than or equal to
- `-gt`:  is greater than
- `-ge`:  is greater than or equal to

While these flags don't exactly make use of the mathematical notation that we are used to, they do come built in with the if command. 

##### Expansions

Flags are useful, however, often times you may want to just use the mathematical notation that you've become accustomed to. If you were to attempt to use this notation without anything additional, you'd see: 

`badMathIf.sh`

```bash
#!/bin/bash

first=1
second=2

echo give me a number please:
read first
echo give me another number:
read second

if [[ $first > $second  ]]
then
 echo $first is greater than $second!
else
 echo $second is greater than $first!
fi

echo How curious?
```

This notation looks correct at first glance, and it is "correct" in that it's not wrong. It's just not doing exactly what we're expecting: 

```bash
./badMathIf.sh
```

> give me a number please:
>
> 10
>
> give me another number:
>
> 5
>
> 5 is greater than 10!
>
> How curious?

What's happening above is that we're comparing the strings "5" and "10". When you place strings into alphabetical order, you only look at the first letter (and then look at the following letters if the strings have matching characters). Luckily for us, we can use expansion notation to treat these values as numerical ones: 

`goodMathIf.sh`

```bash
#!/bin/bash

first=1
second=2

echo give me a number please:
read first
echo give me another number:
read second

if (( $first > $second  ))
then
 echo $first is greater than $second!
else
 echo $second is greater than $first!
fi

echo How curious?
```

Notice in the code above that the only thing that has changed is that we've changed the notation of our `if`'s test expression from `[[]]` to `(())`.  Be extremely careful that you remember what to surround your test expressions with. 



### 5.12 Break and Continue

When you find yourself in a loop, there are often times certain conditions that you may wish to either exit the loop entirely, or just move onto the next iteration. That's what break and continue are for. `break` is a command that kicks you out of the loop entirely, whereas `continue` moves onto the next iteration. 

Suppose we have a loop with a menu: 

`continueBreak.sh`

```bash
#!/bin/bash

function printMenu () {
    echo Please select one of the following:
    echo 1. Reset the variables back to their original values.
    echo 2. See the output of \$first+\$second
    echo 3. See the output of \$\(\(first + second\)\)
    echo 4. Exit the program
    echo
}

originalValueFirst=1
originalValueSecond=2
first=$originalValueFirst
second=$originalValueSecond
userInput='5'

echo This program will print the values of the two variabls \"first\" and \"second\"
echo After the menu is displayed and the commands are executed,
echo the variables \"first\" and \"second\" will be incremented

while [[ "infinite" ]]
do
    echo The two values are currently:
    echo first:$first    second:$second
    echo
    printMenu
    read userInput
    echo

    case $userInput in
        1)
           first=$originalValueFirst
           second=$originalValueSecond
           continue
           ;;
        2)
           strVal=$first+$second
           echo first+second \= $strVal
           ;;
        3)
           mathVal=$((first+second))
           echo \$\(\(first+second\)\)\=\> $first + $second \= $mathVal
	         ;;
        4) break
           ;;
        *) echo Bad input! Please see the menu.
           continue
           ;;
    esac

    echo Incrementing the values...
    ((first++))
    ((second++))
    echo;echo
done

echo The final values are:
echo first: $first        second:$second
echo Thank you so much for using our script!
```



So in this above script, we have a function for printing a basic menu. We then have our variable list (along with original values for easy resetting). Inside the while loop (that is an infinite loop because it's always returning true for a string with any value) we print the data and then get a user's input. From there we decide what to do. 

At option `1`, we reset the data and then continue. What does that mean? When we continue, we go immediately back to the beginning of the while loop! At options  `2`  and `3` we wind up illustrating how bash commands work. Option `4` breaks out of loop entirely, and moves to line `57`, and the default `*` continues (i.e. moves back to the beginning of the while loop). 

For the options that did not `break` or `continue`, we then increment the values with the increment operator within the math expansion! 



### 5.13 Working with Files:

In our earlier script, `versionBump.sh` we initially checked to see fi a file existed with the `-f` flag inside of our if. There are a number of other flags that we can use inside of our if statements to ensure that we can even access a file, write to a file, etc: 

- `-r`: Determine if the file is readable
- `-w`: Determine if the file is writable
- `-x`: Determine if the file is executable
- `-f`: Determine if the file is an ordinary file
- `-e`: Determine if the file exists
- `-s`: Determine if the file has a size (that is, if the file has any contents)
- `-o`: Determine if the file is owned by the user
- `-d`: Determine if the file is a directory

Let's write a script to tell us in plain text what a file is: 

```bash
#!/bin/bash


fileName=$1

### File types:
if [ -e ./$fileName ]; then
        echo $fileName exists
fi

if [ -f ./$fileName ]; then
        echo $fileName is an ordinary file
fi

if [ -d ./$fileName ]; then
        echo $fileName is a directory
fi

if [ -o ./$fileName ]; then
        echo $fileName is owned by $USER
fi


### Contents and permissions
if [ -s ./$fileName ]; then
        echo $fileName has contents
fi

if [ -r ./$fileName ]; then
        echo $fileName is readable
fi

if [ -w ./$fileName ]; then
        echo $fileName is writable
fi

if [ -x ./$fileName ]; then
        echo $fileName is executable
fi

```

If we then attempt to run this file on any other files or directories, we can then in plain text what our permissions are, and whether or not the file exists and is a directory or an ordinary file: 

```bash
./fileType.sh example.c
```

> example.c exists
>
> example.c is an ordinary file
>
> example.c has contents
>
> example.c is readable
>
> example.c is writable

Or for something like a directory: 

```bash
./fileType.sh sampleDir
```

> sampleDir/ exists
>
> sampleDir/ is a directory
>
> sampleDir/ has contents
>
> sampleDir/ is readable
>
> sampleDir/ is writable
>
> sampleDir/ is executable



What distinguishes an "ordinary file" is that the file is an executable or some text file. Non ordinary files are links and directories. 

### 5.14 Variables

We've already started working with variables, quite a bit. So far, though, the variables we've seen are from positional parameters and basic variables within the shell scripts, and environment variables from the shell itself. When declaring a variable, you can use the syntax: 

```bash
variableName='someValue'
```

Depending on what falls into the place of "someValue", you can set the variable name as a string value, or a more complicated value such as something returned from an expansion of some kind. 

You can additionally use the `declare` keyword to declare placeholders.

-  `-i` sets integer values
-  `-r` is read only (think for making constants)
- `-a` declares an array type
- `-x` declares value exported to the environment
- `-p` prints the variable's declared purpose

`declareExample.sh`

```bash
declare -i integerValue 
integerValue=23
declare -p integerValue


someValue="I am a string"
declare -r someValue
#someValue="What if I changed?"
declare -p someValue

declare -a array
array="can I attempt to make an array without values?"
array="Another?"
declare -p array

declare -x environmentVar
environmentVar="I AM IN THE ENVIRONMENT NOW!"
declare -p environmentVar

```



### 5.15 Arrays

When creating an array, you can use the `declare` syntax, however you can implicitly create an array by using:

```bash
someArrayName=("element0", "element1", "etc")
```

To access the elements, you use the indexed values: 

```bash
echo $someArrayName[0]
```

To add a new element into the array, you can use the `+=` syntax: 

```bash
someArrayName+=("element3")
```



Let's look at an how to work with arrays: 

`arrayExample.sh`

```bash
#!/bin/bash

emptyArray=()

emptyArray+=("someElement")
emptyArray+=("otherElement")

echo Echoing emptyArray = $emptyArray
echo Echoing all of the arrays contents: ${emptyArray[*]}
echo Getting the length of the array is with ${#emptyArray[*]}


echo You can add elements to any index of an array, however:
emptyArray[9]="what?"

echo
echo To iterate over an array, you will need to:
for ((i=0; i < ${#emptyArray[*]}; i++ ))
do
        echo element at i$i = ${emptyArray[$i]}
done
echo
echo what happened to \"what?\" ?? We need to access the 9th index:
echo emptyArray\[9\]  = ${emptyArray[9]}
echo


echo And to reset the indices of an array:
resetArray+=( "${emptyArray[@]}" )

echo empty array length is: ${#emptyArray[*]}
echo Reset array length is ${#resetArray[*]}

for singleElement in "${emptyArray[@]}"
do
        echo single element: $singleElement
done
```

The above prints out: 

> Echoing emptyArray = someElement
>
> Echoing all of the arrays contents: someElement otherElement
>
> Getting the length of the array is with 2
>
> You can add elements to any index of an array, however:
>
> 
>
> To iterate over an array, you will need to:
>
> element at i0 = someElement
>
> element at i1 = otherElement
>
> element at i2 =
>
> 
>
> what happened to "what?" ?? We need to access the 9th index:
>
> emptyArray[9] = what?
>
> 
>
> And to reset the indices of an array:
>
> empty array length is: 3
>
> Reset array length is 3
>
> single element: someElement
>
> single element: otherElement
>
> single element: what?



It's also possible to read array elements in with `read`: 

`readArrayElements.sh`

```bash
#!/bin/bash

echo Words separated by a space are now array elements
read -a arr

for value in "${arr[@]}"
do
        echo  the value is: $value
done
```

When running this program we get to enter space delimited array elements: 

```bash
./readArrayElements.sh
```

> Words separated by a space are now array elements
>
> i have a neat array making sentence
>
> the value is: i
>
> the value is: have
>
> the value is: a
>
> the value is: neat
>
> the value is: array
>
> the value is: making
>
> the value is: sentence



### 5.16 Variable Modifiers

It's possible to use modifiers on top of variables to make your code do more. These modifiers can do multiple things, from checking to see if the variable exists to grabbing specific substrings: 

- `${someVariable:-defaultValue}`: This **returns** the default value if `someVariable` doesn't exist (or has no value). 
- `${someVariable:=defaultValue}`: This **sets** the value of `someVariable` to `defaultValue` if `someVariable` doesn't exist (or has no value)
- `${someVariable:?errorMessage}`: If `someVariable` doesn't exist, the program exits and prints `errorMessage` to the std error



#### Existential Modifiers

An example of using the above four is: 

`unsetVarExamples.sh`

```bash
#!/bin/bash

unsetVar1=''
unsetVar2=''


var1=${unsetVar1:-somethingElse}
echo var1 is $var1
echo

${unsetVar1:="echo I am new!"}
echo unsetVar1 is now $unsetVar1
echo

${unsetVar3:?"Throw an error and exit!"}
echo Did you \exit?
```

Notice in the above that there are two types of variables that we're using that are technically "unset" or "null". First we have the two declared variables that are empty strings. That's just as good as being unset or null.  Secondly, these work just the same with variables that have never been declared whatsoever like in line 15. 



#### Substring Modifiers

These variable modifiers allow for us to interact with specific chunks of the variables themselves: 

- `${someVariable:offset:length}`: This modifier grabs a substring from `someVariable` staring from the offset and going to length (or the end if no length)
- `${someVariable#pattern}` OR  `${someVariable##pattern}` deletes a pattern with matching prefix
- `${someVariable%pattern}` OR `${someVariable%%pattern}` deletes a pattern with the matching suffix
- `${someVariable/pattern/newString}` finds and replaces the substring matching `pattern` with `newString`



`substringModifiers.sh`

```bash
#!/bin/bash

someVariable="I am a long variable."

echo ${someVariable:7:4}

echo ${someVariable#I am a }

echo ${someVariable%iable.}

echo ${someVariable/long/way\ cool}
```

Seeing this code in action: 

```bash
./substringModifiers.sh
```

> long
>
> long variable.
>
> I am a long var
>
> I am a way cool variable.



It is possible to apply these patterns to arrays. When using the offset/length, you'll wind up with subarray. All other methods will map over the array and apply the string manipulations to each array element. 

#### Parsing Strings

Often times, it's likely that you'll come across a string that needs to be parsed over and split on a specific delimiter. You can do this with the internal field separator, or `IFS`. The general syntax for using `IFS` is done in conjunction with read: 

```bash
IFS=',' #setting space as comma
read -ra arrayOfValuesFromDelimitedString <<<"$commaSeparatedString" 
```

Previously we were working on a shell script, `versionBump.sh`. Now that we know how to use arrays, and we know hot to use mathematical expansions, and we know how to use sed. Let's put all of this together for a final working version bump: 

```bash
File version is now 1 0 0
[mjlny2@delmar ch5]$ vim versionBump.sh
#!/bin/bash
RED_COLORATION='\033[0;31m' #red color



versionType=$1
fileName=$2

echo You wish to increment the $versionType version for $fileName

if [[ ! -f ./$fileName ]]; then
    printf "$fileName ${RED_COLORATION}does not exist.${NO_COLORATION}\n"
    exit
fi



currentVersion=$(sed -n 's/VERSION=//p' $fileName)
echo The current version of $fileName is $currentVersion

IFS='.'
read -ra versionArray <<< "$currentVersion"

echo Major ${versionArray[0]}
echo Minor ${versionArray[1]}
echo Patch ${versionArray[2]}

major=${versionArray[0]}
minor=${versionArray[1]}
patch=${versionArray[2]}


case $versionType in
[Mm]ajor)
    echo Major version bump:
    ((major++))
    ;;
[Mm]inor)
    echo Minor version bump:
    ((minor++))
    ;;
[Pp]atch)
    echo Patch version bump:
    ((patch++))
    ;;
*)  printf "${RED_COLORATION}Bad version bump input.${NO_COLORATION}\n"
    echo The possible input values for version type are: "Major" \| "Minor" \| "Patch"
    exit
    ;;
esac

newVersion="$major"'.'"$minor"'.'"$patch"

sed -i "s/$currentVersion/$newVersion/" "$fileName"
echo File version is now $newVersion
```

In the above, we've split the version into three separate variables, `major`, `minor`, and `patch`, wherein we then update the version type in the case statement. From there we recreate the version string and then supply a new version string with `sed` and it's `-i` inline flag. 



### 5.18 Functions

We've already seen some functions, but we've only used them to act as a way to quickly print a menu and keep our code mildly uncluttered. Functions act like their own independent scripts. Looking at the syntax again: 

```bash
function someFunc () { commandlist }
```

#### Parameters:

You may see the function syntax and think it's similar to c-style languages that can define parameters within the parentheses but that will just cause errors. Functions take *positional parameters* just like a full shell script. Take, for example, the script `functionArguments.sh`. We can pass an argument into this script, and then have that script pass an argument of another kind to a function: 

`functionArguments.sh`

```bash
#!/bin/bash

function someFuncWithArgs () {
	echo the first \function argument is $1
	echo the second is $2
}

echo The first argument to the script is $1
echo The second argument to the script is $2

someFuncWithArgs neato mosquito
```

Now, when executing this script with the following parameters: 

``` bash
./functionArguments.sh cool beans
```

> The first argument to the script is cool
>
> The second argument to the script is beans
>
> the first function argument is neato
>
> the second is mosquito

Think of functions as their own subscripts. Even though we're using `$1` and `$2` at lines 4,5 and 8,9, depending on the context, those positional parameters are referring to 2 completely different sets of data. 

#### Return Values

Functions all have a return value. All functions (and shell scripts for that matter) have a return value of some integer value 0-255.  You can specify which integer value to return with the `return` keyword. However, it's unlikely that you'll always want to return a simple integer (also using the return value for the status for your own purposes is mildly unwise).

 There are a number of ways to interact with data from functions. The first is the most convenient in that, it's exactly how we return data to the command line of any shell script: `echo`. 

```bash
#!/bin/bash

function noEchoBack() {
	results='some results!'
}

function echoBack() {
	otherResults="echoBack results."
	echo "$otherResults"
}

firstFuncResults=$(noEchoBack)
secondFuncResults=$(echoBack)

echo first results are: $firstFuncResults
echo second results are: $secondFuncResults

echo but can I also see what is stored \in $results or $otherResults ? 
```

You could also consider using global variables to pass yours back. However, global variables can be dangerous if you're not paying attention. 



### 5.19 Redefining Bash Built-In Functions

It is possible to redefine bash built in functions. It's strongly recommended that you don't do this. 

### 5.20 Example Scripts

Please take the time to go through the sample scripts! 

### 5.21 Debugging! 

When you are working on a shell script, it's likely the case that you'll run into issues. Luckily, if a command fails to execute because of a syntax error, it will automatically be printed to the shell. However, that doesn't work for logical errors. To see how your program executes, you can trace each of its steps with the `set -x` command to turn tracing on (or `bash -x someScript.sh`). Let's try it with our `versionBump.sh`

```bash
set -x 
./versionBump.sh minor versionedProgram.sh
```

> +./versionBump.sh minor versionedProgram.sh
> You wish to increment the minor version for versionedProgram.sh
> The current version of versionedProgram.sh is 2.0.0
> Major 2
> Minor 0
> Patch 0
> Minor version bump:
> File version is now 2 1 0
> Filename is still versionedProgram sh
> File version is now 2 1 0
> ++ printf '\033]0;%s@%s:%s\007' mjlny2 delmar '~/2750Materials/module3/ch5'

Using the `bash -x someScript.sh` format can be tricky given that the position of the parameters shifts. Your best bet is to use this format for scripts that don't take arguments. 

### 5.22 Error and Interrupt Handling 

In order to ensure that your scripts fail gracefully and can properly assess interrupts, you'll need to properly handle these details. 

#### Error Handling

Depending on the type of error, a script may or may not halt. If your script has a syntax error, then you'll need to fix it. When regular commands fail, however, their output is logged, and the script continues, which is not always ideal. To ensure that these errors are caught, making us of the return values can be helpful.

A good example of when you'd want to gracefully fail is in a deploy script, which typically will bump the version, build the project ,and then deploy it to the cloud (or whatever service it is hosted on). 

`failedVersionBump.sh`

```bash
#!/bin/bash

fileName='someFile.whatever'

echo Bumping $fileName version of $1 and deploying to the cloud.

./versionBump.sh $1 $fileName

echo Build Phase: 
#do the building

echo Deployment Phase:
#do the doployment commands
```

In the above code, if we fail on the `versionBump.sh` command, we'll still keep executing.  We want everything to run smoothly. We can instead use the return values of programs to ensure that we get to deal with failed executions: 

`gacefulFailure.sh`

```bash
#!/bin/bash

fileName='someFile.whatever'

echo Bumping $fileName version of $1 and deploying to the cloud.

./versionBump.sh $1 $fileName

echo Build Phase: 
#do the building

echo Deployment Phase:
#do the doployment commands
```

#### Interrupt Handling

Interrupt handling is something slightly different. While we haven't covered signals by any significant measure, we have seen the `kill` command (and we've used the `ctrl + c` command). These are signals, which we'll get into significantly more deeply in chapter 11. Here, though we can at least introduce the command `trap` which can take a specific signal and doing something with that signal. The general syntax looks like: 

```bash
trap command signal
```

In this command we can do anything we wish. For now, let's ensure that our extremely important program `countAndWait.sh` can execute without being interrupted: 

```bash
#!/bin/bash

trap "The program must complete before interruption or termination." SIGTERM SIGINT

for (( i=0; i<15; i++))
do
        echo $1
        sleep 1
done
```

Now, if we run this program and attempt to interrupt it, we'll see: 

```bash
./countAndWait.sh
```

> the value of 0
>
> the value of 1
>
> the value of 2
>
> ^CThe program must complete before interruption or termination.
>
> the value of 3
>
> ^CThe program must complete before interruption or termination.
>
> the value of 4
>
> ^CThe program must complete before interruption or termination.
>
> the value of 5
>
> ^CThe program must complete before interruption or termination.
>
> the value of 6
>
> ^CThe program must complete before interruption or termination.
>
> the value of 7
>
> ^CThe program must complete before interruption or termination.
>
> the value of 8
>
> ^CThe program must complete before interruption or termination.
>
> the value of 9
>
> the value of 10
>
> ^CThe program must complete before interruption or termination.
>
> the value of 11
>
> the value of 12
>
> the value of 13
>
> the value of 14

