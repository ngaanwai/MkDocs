---
title: shell scripting
tags: [computer]

### Bash shell

The default shell for many Linux distros is the GNU Bourne-Again Shell (bash). Bash is succeeded by Bourne shell (`sh`).

When you first launch the shell, it uses a startup script located in the `.bashrc` or `.bash_profile` file which allows you to customize the behavior of the shell.

When a shell is used interactively, it displays a `$` when it is waiting for a command from the user. This is called the shell prompt.

`[username@host ~]$`

If shell is running as root, the prompt is changed to `#`. The superuser shell prompt looks like this:

`[root@host ~]#`

### Environment

Login shells read one or more startup files as shown below:

|**File**|**Contents**|
|---|---|
|`/etc/profile`|A global configuration script that applies to all users.|
|`~/.bash_profile`|A user's personal startup file. Can be used to extend or override settings in the global configuration script.
|`~/.bash_login`|If `~/.bash_profile` is not found, bash attempts to read this script.
|`~/.profile`|If neither `~/.bash_profile` nor `~/.bash_login` is found, bash attempts to read this file. This is the default in Debian-based distributions, such as Ubuntu.

Non-login shell sessions read the following startup files:

|**File**|**Contents**|
|---|---|
|`/etc/bash.bashrc`|A global configuration script that applies to all users.
|`~/.bashrc`|A user's personal startup file. Can be used to extend or override settings in the global configuration script.

In addition to reading the startup files above, non-login shells also inherit the environment from their parent process, usually a login shell.

Take a look at your system and see which of these startup files you have. Remember— since most of the file names listed above start with a period (meaning that they are hidden), you will need to use the “-a” option when using ls.

The `~/.bashrc` file is probably the most important startup file from the ordinary user’s point of view, since it is almost always read. Non-login shells read it by default and most startup files for login shells are written in such a way as to read the `~/.bashrc` file as well.

If we take a look inside a typical `.bash_profile` (this one taken from a CentOS system), it looks something like this:
```
# .bash_profile 
# Get the aliases and functions 
if [ -f ~/.bashrc ]; then
  . ~/.bashrc 
fi 
# User specific environment and startup programs 
PATH=$PATH:$HOME/bin 
export PATH
```


Lines that begin with a “#” are comments and are not read by the shell. These are there for human readability. The first interesting thing occurs on the fourth line, with the following code:
```
if [ -f ~/.bashrc ]; then
  . ~/.bashrc 
fi
```

This is called an _if compound command_, which we will cover fully in a later lesson, but for now we will translate:

If the file "~/.bashrc" exists, then read the "~/.bashrc" file.

We can see that this bit of code is how a login shell gets the contents of `.bashrc`. The next thing in our startup file does is set the PATH variable to add the `~/bin` directory to the path.

Lastly, we have:

`export PATH`

The `export` command tells the shell to make the contents of the PATH variable available to child processes of this shell.



### Scripts start with a bash bang.

Scripts are also identified with a `shebang`. Shebang is a combination of `bash #` and `bang !`  followed the the bash shell path. This is the first line of the script. Shebang tells the shell to execute it via bash shell. Shebang is simply an absolute path to the bash interpreter.

Below is an example of the shebang statement.

```bash
#! /bin/bash
```

The path of the bash program can vary. We will see later how to identify it.

## How to Create Your First Bash Script

Let's create a simple script in bash that outputs `Hello World`.

### Create a file named hello_world.sh

```bash
touch hello_world.sh
```

### Find the path to your bash shell.

```bash
which bash
```

### Write the command.

We will `echo` "hello world" to the console.

Our script will look something like this:

```bash
#! usr/bin/bash
echo "Hello World"
```

### Run the script.

You can run the script in the following ways:

`bash hello_world.sh`.


## The Basic Syntax of Bash Scripting

### How to define variables

We can define a variable by using the syntax `variable_name=value`. To get the value of the variable, add `$` before the variable.

```bash
#!/bin/bash
# A simple variable example
greeting=Hello
name=Tux
echo $greeting $name
```

### Arithmetic Expressions

Below are the operators supported by bash for mathematical calculations:

|OPERATOR|USAGE|
|---|---|
|`+`|addition
|`-`|subtraction
|`*`|multiplication
|`/`|division
|`**`|exponentiation
|`%`|modulus

Numerical expressions can also be calculated and stored in a variable using the syntax below:

`var=$((expression))`

Let's try an example.

```bash
#!/bin/bash

var=$((3+9))
echo $var
```

Fractions are not correctly calculated using the above methods and truncated.

For **decimal calculations**, we can use `bc` command to get the output to a particular number of decimal places. `bc` (Bash Calculator) is a command line calculator that supports calculation up to a certain number of decimal points.

`echo "scale=2;22/7" | bc`

Where `scale` defines the number of decimal places required in the output.

### How to read user input

Sometimes you'll need to gather user input and perform relevant operations.

In bash, we can take user input using the `read` command.

```
read variable_name
```

To prompt the user with a custom message, use the `-p` flag.

`read -p "Enter your age" variable_name`

**Example:**

```bash
#!/bin/bash

echo "Enter a numner"
read a

echo "Enter a numner"
read b

var=$((a+b))
echo $var
```

### Numeric Comparison logical operators

Comparison is used to check if statements evaluate to `true` or `false`. We can use the below shown operators to compare two statements:

|OPERATION|SYNTAX|EXPLANATION|
|---|---|---|
|Equality|num1 -eq num2|is num1 equal to num2
|Greater than equal to|num1 -ge num2|is num1 greater than equal to num2
|Greater than|num1 -gt num2|is num1 greater than num2
|Less than equal to|num1 -le num2|is num1 less than equal to num2
|Less than|num1 -lt num2|is num1 less than num2
|Not Equal to|num1 -ne num2|is num1 not equal to num2

**Syntax**:

```bash
if [ conditions ]
    then
         commands
fi
```

**Example**:

Let's compare two numbers and find their relationship:

```bash
read x
read y

if [ $x -gt $y ]
then
echo X is greater than Y
elif [ $x -lt $y ]
then
echo X is less than Y
elif [ $x -eq $y ]
then
echo X is equal to Y
fi
```

### Conditional Statements (Decision Making)

Conditions are expressions that evaluate to a boolean expression (`true` or `false`). To check conditions, we can use `if`, `if-else`, `if-elif-else` and nested conditionals.

The structure of conditional statements is as follows:

-   `if...then...fi` statements
-   `if...then...else...fi` statements
-   `if..elif..else..fi`
-   `if..then..else..if..then..fi..fi..` (Nested Conditionals)

**Syntax**:

```bash
if [[ condition ]]
then
	statement
elif [[ condition ]]; then
	statement 
else
	do this by default
fi
```

To create meaningful comparisons, we can use AND `-a` and OR `-o` as well.

The below statement translates to: If `a` is greater than 40 and `b` is less than 6.

`if [ $a -gt 40 -a $b -lt 6 ]`

**Example**: Let's find the triangle type by reading the lengths of its sides.

```bash
read a
read b
read c

if [ $a == $b -a $b == $c -a $a == $c ]
then
echo EQUILATERAL

elif [ $a == $b -o $b == $c -o $a == $c ]
then 
echo ISOSCELES
else
echo SCALENE

fi
```

### Looping and skipping

For loops allow you to execute statements a specific number of times.

#### Looping with numbers:

In the example below, the loop will iterate 5 times.

```bash
#!/bin/bash

for i in {1..5}
do
    echo $i
done
```

#### Looping with strings:

We can loop through strings as well.

```bash
#!/bin/bash

for X in cyan magenta yellow  
do
	echo $X
done
```

#### While loop

While loops check for a condition and loop until the condition remains `true`. We need to provide a counter statement that increments the counter to control loop execution.

In the example below, `(( i += 1 ))` is the counter statement that increments the value of `i`.

**Example:**

```bash
#!/bin/bash
i=1
while [[ $i -le 10 ]] ; do
   echo "$i"
  (( i += 1 ))
done
```

### Reading files

Suppose we have a file `sample_file.txt` 

We can read the file line by line and print the output on the screen.

```bash
#!/bin/bash

LINE=1

while read -r CURRENT_LINE
	do
		echo "$LINE: $CURRENT_LINE"
    ((LINE++))
done < "sample_file.txt"
```

### How to execute commands with back ticks

If you need to include the output of a complex command in your script, you can write the statement inside back ticks.

#### Syntax:

```
var= `commands`
```

**Example**: Suppose we want to get the output of a list of mountpoints with `tmpfs` in their name. We can craft a statement like this: `df -h | grep tmpfs`.

To include it in the bash script, we can enclose it in back ticks.

```bash
#!/bin/bash

var=`df -h | grep tmpfs`
echo $var
```

### How to get arguments for scripts from the command line

It is possible to give arguments to the script on execution.

`$@` represents the position of the parameters, starting from one.

```bash
#!/bin/bash

for x in $@
do
    echo "Entered arg is $x"
done
```

Run it like this:

`./script arg1 arg2`

## How to Automate Scripts by Scheduling via cron Jobs

Cron is a job scheduling utility present in Unix like systems. You can schedule jobs to execute daily, weekly, monthly or in a specific time of the day. Automation in Linux heavily relies on cron jobs.

Below is the syntax to schedule crons:

```bash
# Cron job example
* * * * * sh /path/to/script.sh
```

Here, `*` represent represents minute(s) hour(s) day(s) month(s) weekday(s), respectively.

Below are some examples of scheduling cron jobs.

|SCHEDULE|SCHEDULED VALUE|
|---|---|
|5 0 * 8 * |At 00:05 in August.
|5 4 * * 6|At 04:05 on Sunday.
|0 22 * * 1-5|At 22:00 on every day-of-week from Monday through Friday.
