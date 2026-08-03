A truly powerful feature of the shell is the capability to redirect the input and output
of commands to and from other commands and files. To allow commands to be strung
together, the shell uses metacharacters. A metacharacter is a typed character that has special
meaning to the shell for connecting commands or requesting expansion.
Metacharacters include the pipe character (|), ampersand (&), semicolon (;), right parenthesis
()), left parenthesis ((), less than sign (<), and greater than sign (>).

### Background commands
Some commands can take a while to complete. Sometimes, you may not want to tie up your
shell waiting for a command to finish. In those cases, you can have the commands run in
the background by using the ampersand (&).
```bash
$ troff -me verylargedocument | lpr &
```

### Sequential commands
Sometimes, you may want a sequence of commands to run, with one command completing
before the next command begins. You can do this by typing several commands on the same
command line and separating them with semicolons (;):
```bash
$ date ; troff -me verylargedocument | lpr ; date
```
### Piping between commands
The pipe (|) metacharacter connects the output from one command to the input of another
command. This lets you have one command work on some data and then have the next
command deal with the results. Here is an example of a command line that includes pipes:
```bash
$ cat /etc/passwd | sort | less
```
```bash
$ gunzip < /usr/share/man/man1/grep.1.gz | nroff -c -man | less
```
### Expanding commands
With command substitution, you can have the output of a command interpreted by the shell instead of by the command itself. In this way, you can have the standard output of a
command become an argument for another command. The two forms of command substitution
are $(command) and ``command`` (backticks, not single quotes).
The command in this case can include options, metacharacters, and arguments. The following
is an example of using command substitution:
```bash
$ vi $(find /home | grep xyzzy)
```

### Expanding arithmetic expressions
Sometimes, you want to pass arithmetic results to a command. There are two forms that
you can use to expand an arithmetic expression and pass it to the shell: $[expression]
or $(expression). The following is an example:
```bash
$ echo "I am $[2020 - 1957] years old."
I am 63 years old.
```
The shell interprets the arithmetic expression first (2020 - 1957) and then passes that
information to the echo command. The echo command displays the text with the results
of the arithmetic (63) inserted.
Here’s an example of the other form:
```bash
$ echo "There are $(ls | wc -w) files in this directory."
There are 14 files in this directory.
```
This lists the contents of the current directory (ls) and runs the word count command to
count the number of files found (wc -w). The resulting number (14, in this case) is echoed
back with the rest of the sentence shown.

### Expanding variables
Variables that store information within the shell can be expanded using the dollar sign ($)
metacharacter. When you expand an environment variable on a command line, the value of
the variable is printed instead of the variable name itself, as follows:
```bash
$ ls -l $BASH
-rwxr-xr-x. 1 root root 1219248 Oct 12 17:59 /usr/bin/bash
```
Using $BASH as an argument to ls -l causes a long listing of the bash command to
be printed.



