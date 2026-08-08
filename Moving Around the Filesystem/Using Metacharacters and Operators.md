To save you some keystrokes and enable you to refer easily to a group of files, the bash shell
lets you use metacharacters. Anytime you need to refer to a file or directory, such as to
list, open, or remove it, you can use metacharacters to match the files you want. 
- Here are some useful metacharacters for matching filenames:
 - * Matches any number of characters.
 - ? Matches any one character.
 - [...] Matches any one of the characters between the brackets, which can include a hyphenseparated range of letters or numbers.

### Using file redirectly metacharacters
Commands receive data from standard input and send it to standard output. Using pipes
(described earlier), you can direct standard output from one command to the standard
input of another. With files, you can use less than (<) and greater than (>) signs to direct
data to and from files. 
- Here are the file-redirection characters:
  - `<` Directs the contents of a file to the command. In most cases, this is the default action expected by the command and the use of the character is optional; using less bigfile is the same as less < bigfile.
  - `>` Directs the standard output of a command to a file. If the file exists, the content of that file is overwritten.
  - `2>` Directs standard error (error messages) to the file.
  - `&>` Directs both standard output and standard error to the file.
  - `>>` Directs the output of a command to a file, adding the output to the end of the existing file.`
### Important Example of Metacharacters:-
Another type of redirection, referred to as here text (also called here document), enables you to type text that can be used as standard input for a command. Here documents involve entering two less-than characters (<<) after a command, followed by a word. All typing following that word is taken as user input until the word is repeated on a line by itself. Here is an example:
```bash 
$ mail root cnegus rjones bdecker << thetext
> I want to tell everyone that there will be a 10 a.m.
> meeting in conference room B. Everyone should attend.
>
> -- James
> thetext
$
```
This example sends a mail message to root, cnegus, rjones, and bdecker usernames. The text entered between `<<thetext` and `thetext` becomes the content of the message.

- A common use of here text is to use it with a text editor to create or add to a file from
within a script:
```bash 
/bin/ed /etc/resolv.conf <<resendit
a
nameserver 100.100.100.100
.
w
q
resendit
```
With these lines added to a script run by the root user, the ed text editor adds the IP
address of a DNS server to the /etc/resolv.conf file.

### Using brace expansion characters
By using curly braces ({}), you can expand out a set of characters across filenames, directory
names, or other arguments to which you give commands. For example, if you want to
create a set of files such as memo1 through memo5, you can do that as follows:
```bash
$ touch memo{1,2,3,4,5}
$ ls
memo1 memo2 memo3 memo4 memo5
```
The items that are expanded don’t have to be numbers or even single digits. For example,
you could use ranges of numbers or digits. You could also use any string of characters, as
long as you separate them with commas. Here are some examples:
```bash
$ touch {John,Bill,Sally}-{Breakfast,Lunch,Dinner}
$ ls
Bill-Breakfast Bill-Lunch John-Dinner Sally-Breakfast Sally-Lunch
Bill-Dinner John-Breakfast John-Lunch Sally-Dinner
$ rm -f {John,Bill,Sally}-{Breakfast,Lunch,Dinner}
$ touch {a..f}{1..5}
$ ls
a1 a3 a5 b2 b4 c1 c3 c5 d2 d4 e1 e3 e5 f2 f4
a2 a4 b1 b3 b5 c2 c4 d1 d3 d5 e2 e4 f1 f3 f5
```
In the first example, the use of two sets of braces means John, Bill, and Sally each have
filenames associated with Breakfast, Lunch, and Dinner. If I had made a mistake, I could
easily recall the command and change touch to `rm -f`to delete all of the files. In the
next example, the use of two dots between letters a and f and numbers 1 and 5 specifies
the ranges to be used. Note the files that were created from those few characters.
- One more example:
``` bash
mkdir –p World/{India/{Hyd,Bang},AUS/{Sydney,Perth},USA/{Tampa,NYC}}
```
Check it by using tree command or ls –R command

<img width="938" height="343" alt="image" src="https://github.com/user-attachments/assets/8977f78e-f989-469a-a989-4844e3ff7c9e" />

## Deep Dive into redirection metacharaters:-
1. The Core Concept (File Descriptors)
In Linux, everything is a file. When a shell runs a command, it inherits three standard open file descriptors (streams) from its parent process:

0 – Standard Input (stdin): Where the command reads input (default = your keyboard).

1 – Standard Output (stdout): Where the command writes normal output (default = your terminal screen).

2 – Standard Error (stderr): Where the command writes error messages (default = your terminal screen).

Redirection is the act of telling the shell: "Do not use the default file (e.g., the terminal) for this descriptor. Instead, open this specific file and connect the descriptor to it."

2. Basic Redirection Operators (The Syntax)
|Operator|	Meaning|	In-Depth L4 Explanation|
|--------|---------|-------------------------|
|`>`|	Redirect stdout (overwrite)	|Opens the target file in write-only mode, truncates it to zero bytes immediately, and connects FD 1 to it. If the file doesn't exist, it is created.|
|`>>`|	Redirect stdout (append)|	Opens the target file in append mode. The file pointer is placed at the end. If the file doesn't exist, it is created.|
|`2>`|	Redirect stderr (overwrite)	Redirects FD 2 specifically.|
|`2>>`|	Redirect stderr (append)|	Appends FD 2.|
|`<`	|Redirect stdin	|Opens the file in read-only mode and connects it to FD 0. The command reads from this file instead of the keyboard.|
|`<<`|	Here-Document	|Not a file—tells the shell to read the subsequent lines of text (until a delimiter) and feed them as stdin.|
|`<<<`|	Here-String	|Feeds a single string (a word or variable) as stdin to the command.|

L4 Critical Rule: The order of redirections on the command line matters because the shell processes them from left to right.

4. Advanced Redirection: Duplicating & Moving Descriptors (The & magic)
This is where L4-level interviewers dig deep. You use `>&` or `<&` to duplicate file descriptors.

|Syntax	|What it actually does|
|------|------------------------|
|>&file|	Shortcut for 1>file (redirects stdout).|
|&>file|	Redirects both stdout and stderr to the same file (overwrite). Equivalent to `>file 2>&1`.|
|&>>file|	Redirects both stdout and stderr to the same file (append). Equivalent to `>>file 2>&1`.|
|2>&1|	Duplicates FD 2 to wherever FD 1 is currently pointing. (Send stderr to the same place as stdout).|
|1>&2|	Duplicates FD 1 to wherever FD 2 is currently pointing. (Send stdout to the same place as stderr).|
|3>file|	Opens a new file descriptor (FD 3) and points it to file. You can then use >&3 to send output to it.|
|>/dev/null 2>&1|	The classic "silence everything". Redirect stdout to the black hole, then redirect stderr to follow stdout.|

** The Single Most Important L4 Gotcha (The Order): **
Look at these two commands. One works, one fails:

- Correct: command >file 2>&1
  1. Shell opens file and points FD 1 to it.
  2. Shell points FD 2 to wherever FD 1 is pointing (which is now file).
  3. Result: Both go to file.
- Wrong (Classic mistake): command 2>&1 >file
  1. Shell points FD 2 to where FD 1 is currently pointing (the terminal).
  2. Shell opens file and points FD 1 to it.
  3. Result: stdout goes to file, but stderr still goes to the terminal because FD 2 was duplicated before FD 1 was changed!

4. The exec Command (Persistent Redirection)
Normally, redirections only affect the single command they are attached to. If you use exec with no command, you change the redirections for the rest of the current shell session or script.

`exec > /var/log/myscript.log` – All subsequent output from this script goes to the log file.

`exec 2>&1` – Make stderr follow stdout permanently from this point onward.

`exec 3< /tmp/input.txt` – Open FD 3 for reading. You can later read from it using read -u 3 or cat <&3.

`exec 3>&-` – Close FD 3 when you are done (clean up file handles to avoid leaks).

L4 Scenario: You are writing a long-running RHEL daemon script. You would use exec at the very top to redirect all output to syslog or a log file, so you don't have to type `>> $LOGFILE` on every single `echo` command.

5. Advanced Scenarios & Troubleshooting (What Interviewers Love)
Q: "You run my_script.sh > output.log 2>&1. The script fails, but output.log remains empty. Why?"

Answer: The script is writing to FD 3, FD 4, or directly to /dev/tty instead of stdout/stderr. Alternatively, the script flushes its buffer to the terminal and uses isatty() to check if it's interactive. If the binary bypasses stdout and writes directly to the TTY, redirection won't catch it. You would need to use script or screen to capture that, or use strace -e write my_script.sh to see exactly which file descriptors are being written to.

Q: "Explain this command: cat < /etc/hosts > /tmp/hosts_backup.txt. What happens step-by-step?"

Answer:

The shell opens /etc/hosts in read-only mode and attaches it to FD 0 (stdin).
The shell opens /tmp/hosts_backup.txt in write-only mode (truncating it) and attaches it to FD 1 (stdout).
The shell forks and executes /usr/bin/cat.
cat reads from FD 0 and writes to FD 1. The shell handles both files, not cat itself.
Q: "What is the difference between >> file 2>&1 and &>> file?"

Answer: In modern Bash (including RHEL 10), there is no functional difference. &>> is syntactic sugar introduced in Bash 4.0. However, an L4 admin should know that &>> is not POSIX-compliant. If you are writing a script for sh (dash) or maximum portability, you must use >> file 2>&1.

Q: "How do you suppress only the error output of a command, while preserving stdout?"

Answer: command 2>/dev/null

Q: "How do you suppress stdout and keep ONLY the errors?"

Answer: command 1>/dev/null or simply command >/dev/null (since > defaults to FD 1).

Q: "How do you send stdout to one file and stderr to a completely different file?"

Answer: command > /path/to/stdout.log 2> /path/to/stderr.log

6. The Danger of Redirection in Privileged Scripts (Security)
At an L4 interview, you must mention security:

Symlink Attacks: If a script runs as root and does echo "data" > /tmp/userfile, a malicious user could replace /tmp/userfile with a symlink to /etc/shadow. The shell will happily follow the symlink and overwrite /etc/shadow.

Mitigation: Use set -C (noclobber) in your scripts. This prevents > from overwriting existing files (you must use >| to force it).

Better Practice: Always write to a uniquely named temporary file (using mktemp) and then mv it into place, or use flock to manage file locks before writing.

Race Condition: The shell checks permissions and opens the file at the exact moment the redirection is processed. If you do sudo echo "secret" > /etc/securefile, the redirection is executed by your current user's shell, not by sudo. You will get "Permission denied". The correct way is echo "secret" | sudo tee /etc/securefile.

7. The Ultimate L4 One-Liner Challenge
An interviewer might throw this at you: "Write a command that: Reads a list of filenames from filelist.txt, ignores any 'permission denied' errors while reading them, counts the total lines in all files combined, and logs any missing files to errors.log, while printing the final count to the terminal."

The L4 Answer:

bash
xargs -a filelist.txt cat 2> >(grep -v "Permission denied" >> errors.log) | wc -l
Breakdown of why this is an L4 answer:

xargs -a reads from a file cleanly.

2> >(...) is process substitution. It redirects stderr not to a file, but into a subshell that runs grep -v to filter out irrelevant errors and append the rest to errors.log.

The stdout from cat (the file contents) is piped directly to wc -l.

Quick Reference Cheatsheet (Memorize for the Interview)
Need	Command
Silently discard all output	command &>/dev/null or command >/dev/null 2>&1
Save output and print it to screen	`command | tee output.log`
Save output and errors to separate files	command > out.log 2> err.log
Feed a multiline string to a command	cat << EOF \n line1 \n line2 \n EOF
Feed a variable's content as stdin	grep "error" <<< "$LARGE_VARIABLE"
Open a file as FD 3 and read line by line	exec 3< /tmp/file; while read -u 3 line; do echo $line; done
Prevent accidental overwrites	set -C (then use >| to force overwrite)


