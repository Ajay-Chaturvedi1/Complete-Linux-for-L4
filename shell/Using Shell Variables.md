In RHEL 10, shell variables store temporary data like text strings, paths, or numbers to change how the shell operates or to streamline scripts.
###🏷️ 1. Local Variables (Current Shell Only)
- Local variables exist only in the specific terminal session or script where you define them. They disappear when you open a new window.
- Define: Do not use spaces around the equals (=) sign.
```bash
MY_NAME="RedHatUser"
```
Access: Put a dollar sign ($) before the variable name.bashecho $MY_NAME

### 🌍 2. Environment Variables (Passed to Child Processes)
Environment variables are system-wide variables. Any software or script started from your current terminal inherits these variables.
- Define: Use export to make a local variable global.
```bash
export SYSTEM_ROLE="admin"
```
- Check: View all active environment variables.
```bash
printenv
```
###⚡ 3. Built-in RHEL 10 Variables
The Bash shell in RHEL 10 comes pre-configured with helpful system variables:
- $USER: The username of the logged-in person (e.g., root).
- $HOME: The path to your home directory (e.g., /home/root).
- $PWD: Your current working directory.$PATH: The list of directories the system searches when you type a command.

###🔗 4. Advanced Variable Operations
Command Substitution: Save the output of a command directly into a variable using $().
```bash
TODAY=$(date +%F)
echo "Today's date is $TODAY"
```
Brace Protection: Use curly braces {} to separate a variable name from touching other text.
```bash
PREFIX="prod"
echo "${PREFIX}_server"  # Outputs: prod_server
```
ReadOnly Variables: Lock a variable so it cannot be modified or deleted.
```bash
readonly LOG_FILE="/var/log/secure"
```
###🔒 5. Variable Expansion rules (Quoting)
- Double Quotes (" "): Evaluates variables inside. echo "Hello $USER" yields Hello root.
- Single Quotes (' '): Treats text literally. echo 'Hello $USER' yields Hello $USER.

---
### export command chalane se ye variable kaha jaa kar save ho jaata hai
Jab aap Linux (RHEL 10) me export command chalate hain, toh wo variable kisi permanent file (jaise hard disk) par save nahi hota. Wo sirf system ki RAM (Memory) me save hota hai.Ye variable kaha aur kaise save hota hai, uski poori details niche di gayi hain:
1. Environment Space (RAM me)
   - export karne par variable aapke current shell ke Environment Block (RAM ka ek hissa) me chala jata hai. Iska matlab hai ki ab ye variable ek Environment Variable ban chuka hai. Jab tak aapka terminal open hai, ye RAM me rahega. Terminal close karte hi ye delete ho jayega.
2. Child Processes (Naye Programs) me pass hota hai
   - Normal variable aur export kiye gaye variable me yahi sabse bada farq hai:
   - Normal Variable (NAME="Amit"): Sirf usi terminal window me kaam karta hai. Agar aap us terminal ke andar koi script ya naya program chalayenge, toh use ye variable nahi milega.
   - Exported Variable (export NAME="Amit"): Current terminal ke sath-sath, uske andar se shuru hone wale sabhi child processes (jaise naye scripts, commands, ya sub-shells) me bhi copy ho jata hai.

### 🔍 Kaise check karein ki ye kaha save hua?
Aap niche di gayi commands se exported variables ko dekh sakte hain:
Poori list dekhne ke liye:
```bash
printenv
# ya fir
env
```
(Ye commands sirf unhi variables ko dikhati hain jo export ho chuke hain).
RAM ke andar process file me dekhna (Advanced):
- Linux me har process ki jankari `/proc` directory me hoti hai. Aap apne current shell (PID) ke environment block ko is command se dekh sakte hain:
```bash
cat /proc/$$/environ | tr '\0' '\n'
```
(Yaha $$ aapke current terminal ki ID hai. Is list me aapko aapka exported variable saaf dikhega).

### 💾 Agar permanent save karna ho toh?
Kyunki export terminal band hote hi delete ho jata hai, agar aap ise hamesha ke liye save karna chahte hain, toh aapko ise ek configuration file me likhna padega:
- Apni home directory ki `.bashrc` file ko open karein:
```bash
nano ~/.bashrc
```
File ke sabse niche apni export command likh dein:
```bash
export MY_VAR="PermanentValue"
```
File ko save karke close karein, aur changes ko apply karne ke liye ye command chalayein:
```bash
source ~/.bashrc
```

## To delete or remove variables in RHEL 10, you use the built-in `unset`command. This removes the variable from the system's memory (RAM) instantly.
### ❌ 1. Deleting a Normal (Local) Variable
If you created a local variable, running unset will completely erase it from the current session.
```bash
# 1. Create the variable
MY_VAR="Hello"

# 2. Verify it exists (Outputs: Hello)
echo $MY_VAR

# 3. Delete the variable
unset MY_VAR

# 4. Try to print it again (Outputs nothing/blank)
echo $MY_VAR
```
🌍 2. Deleting an Environment (Exported) Variable
If you used the `export` command earlier, `unset` will erase it from both the current shell and prevent it from passing to any future child processes.
```bash
# 1. Create and export
export PROD_IP="192.168.1.50"

# 2. Delete it
unset PROD_IP

# 3. Verify it is gone from the environment list (Outputs nothing)
printenv | grep PROD_IP
```
### ⚠️ Important Rules to Keep in Mind
- No Dollar Sign ($): Do not use the $ symbol when deleting. Use `unset VAR_NAME`, not unset $VAR_NAME.
- ReadOnly Variables Cannot Be Deleted: If a variable was marked as readonly, unset will fail with an error.
```bash
readonly SECRET_KEY="12345"
unset SECRET_KEY
# Output: bash: unset: SECRET_KEY: cannot unset: readonly variable
```
Permanent Variables: If you saved a variable inside your ~/.bashrc file, running unset only deletes it for the current open terminal window. It will come back the next time you open a new terminal. To delete it permanently, you must manually open the ~/.bashrc file and delete that line.

## .bashrc file or .bash_profile file me differece batao
~/.bashrc aur ~/.bash_profile dono hi Bash shell ki configuration files hain, lekin inka sabse bada difference is baat par depend karta hai ki aap shell me login kaise kar rahe hain.
- In dono ke beech ke main differences niche diye gaye hain:
  1. Core Difference (Login vs Non-Login Shell)
     - ~/.bash_profile (Login Shell ke liye):
       - Ye file sirf tab chalti hai jab aap pehli baar system me login karte hain.
       -  Examples: Jab aap SSH ke zariye remote server par connect karte hain, ya jab aap su - username command chalate hain.
       -  Ye poore session me sirf ek baar execute hoti hai.
     -  /.bashrc (Non-Login Interactive Shell ke liye):
       - Ye file tab chalti hai jab aap login karne ke baad ek naya terminal window open karte hain.
       - Examples: GUI (Gnome/KDE) me desktop par right-click karke Terminal open karna, ya exit kiye bina naya sub-shell shuru karna.
       - Ye har naye terminal window ke sath baar-baar execute hoti hai.
  2. Quick Comparison Table
|Feature|~/.bash_profile|~/.bashrc|
|-------|----------------|--------|
|Kab chalti hai?|Sirf Login ke waqt (Ek baar)|Har naye Terminal window par|
|Kya save karna chahiye?|$PATH extensions, Heavy startup scripts|Custom Aliases, Target Functions, Prompt colors ($PS1)|
|Scope (Aura)|Poore login session ke liye|Sirf specific terminal window ke liye|

  3. Ye dono aapas me kaise connect hoti hain?
RHEL 10 (aur baki Red Hat distributions) me default setting aisi hoti hai ki jab aap login karte hain, toh `~/.bash_profile` automatic tareeke se `~/.bashrc` ko bhi load kar deti hai.
Agar aap apne `~/.bash_profile` ko open karenge, toh aapko usme ye code dikhega:
```bash
# Get the aliases and functions
if [ -f ~/.bashrc ]; then
        . ~/.bashrc
fi
```
Iska matlab: Login karne par `.bash_profile` chalegi, aur wo automatic `.bashrc` ko bhi load kar degi. Lekin naya terminal kholne par sirf `.bashrc` chalegi.

### 🛠️ Best Practice (Aapko apna variable kaha likhna chahiye?)
Variables aur Path ke liye: Agar aap koi environment variable (jaise export JAVA_HOME=/usr/bin/java) save kar rahe hain, toh use `~/.bashrc` me daalna sabse safe aur best hota hai. Isse wo graphical terminal aur SSH dono jagah hamesha available rahega.
Aliases ke liye: Apne shortcuts (jaise `alias ll='ls -lh'`) ko hamesha `~/.bashrc` me hi likhein.

## Interview related questions:
Q2. Explain the difference between single quotes (' ') and double quotes (" ") regarding variable expansion.
- Answer: Single quotes are strict literal quotes. They turn off the special meaning of all metacharacters.
- Double quotes suppress most metacharacters (like * or ?), but they still allow variable substitution ($) and command substitution ($()).
- Example: If USER=root, then echo "$USER" outputs root, but echo '$USER' outputs literal $USER.
Q3. What is the difference between > and >>?
- Answer: Both are output redirection operators, but > overwrites the destination file completely if it already exists, while >> appends (adds) the new output to the end of the file without deleting the existing content.

Q4. What is the difference between a local variable and an environment variable?
- Answer:A local variable is only accessible within the current shell instance where it was defined. Child processes or scripts executed from that shell cannot see it.
- An environment variable (created using the export command) is placed into the environment block in RAM. It is automatically inherited by any child shells, scripts, or programs started from that terminal session.

Q6. What does echo ${USER}_backup do, and why are curly braces used here?
Answer: It prints the username followed by _backup (e.g., root_backup). The curly braces {} are used for brace protection. Without them, Bash would look for a variable named $USER_backup, which does not exist, resulting in blank output.

### Creating and using aliases
Using the alias command, you can effectively create a shortcut to any command and
options that you want to run later. You can add and list aliases with the alias command.
Consider the following examples of using alias from a bash shell:
``` bash
$ alias p='pwd ; ls –CF'
$ alias rm='rm -i'
```
In the first example, the letter p is assigned to run the command `pwd`and then to run
`ls -CF` to print the current working directory and list its contents in column form.

The second example runs the rm command with the -i option each time you type
rm. (This is an alias that is often set automatically for the root user. Instead of just
removing files, you are prompted for each individual file removal. This prevents you from
automatically removing all of the files in a directory by mistakenly typing something
such as rm *.)
While you are in the shell, you can check which aliases are set by typing the alias
command. If you want to remove an alias, use unalias. (Remember that if the alias
is set in a configuration file, it will be set again when you open another shell.)




### TABLE 3.5 Common Shell Environment Variables
|Variable | Description|
|----------|------------|
|BASH |This contains the full pathname of the bash command. This is usually
/bin/bash.|
|BASH_VERSION |This is a number representing the current version of the
bash command.|
|EUID | This is the effective user ID number of the current user. It is assigned
when the shell starts, based on the user’s entry in the /etc/passwd file.
|FCEDIT| If set, this variable indicates the text editor used by the fc command
to edit history commands. If this variable isn’t set, the vi
command is used.|
|HISTFILE | This is the location of your history file. It is typically located at $HOME/.
bash_history.|
|HISTFILESIZE | This is the number of history entries that can be stored. After this
number is reached, the oldest commands are discarded. The default
value is 1000.|
|HISTCMD| This returns the number of the current command in the history list.|
|HOME |This is your home directory. It is your current working directory each
time you log in or type the cd command with any options.|
|HOSTTYPE |This is a value that describes the computer architecture on which
the Linux system is running. For Intel-compatible PCs, the value is
i386, i486, i586, i686, or something like i386-linux. For AMD 64-bit
machines, the value is x86_64.|
|MAIL| This is the location of your mailbox file. The file is typically your username
in the /var/spool/mail directory.|
|OLDPWD| This is the directory that was the working directory before you changed to the current working directory.
|OSTYPE |This name identifies the current operating system. For Fedora Linux,
the OSTYPE value is either linux or linux-gnu, depending on the
type of shell you are using. (Bash can run on other operating systems
as well.)|
|PATH| This is the colon-separated list of directories used to find commands
that you type. The default value for regular users varies for different
distributions but typically includes the following: /bin:/usr/bin:/
usr/local/bin:/usr/bin/X11:/usr/X11R6/bin:~/bin. You need to
type the full path or a relative path to a command that you want to run
which is not in your PATH. For the root user, the value also includes /
sbin, /usr/sbin, and /usr/local/sbin.|
|PPID |This is the process ID of the command that started the current shell (for
example, the Terminal window containing the shell).|
|PROMPT_COMMAND | This can be set to a command name that is run each time before your
shell prompt is displayed. Setting PROMPT_COMMAND=date lists the
current date/time before the prompt appears.|
|PS1| This sets the value of your shell prompt. There are many items that you
can read into your prompt (date, time, username, hostname, and so on).
Sometimes a command requires additional prompts, which you can set
with the variables PS2, PS3, and so on.|
|PWD| This is the directory that is assigned as your current directory. This value
changes each time you change directories using the cd command.|
|RANDOM |Accessing this variable causes a random number to be generated. The
number is between 0 and 99999.|
|SECONDS| This is the number of seconds since the time the shell was started. |
|SHLVL | This is the number of shell levels associated with the current shell
session. When you log in to the shell, the SHLVL is 1. Each time you
start a new bash command (by, for example, using su to become a new
user, or by simply typing bash), this number is incremented.|
|TMOUT | This can be set to a number representing the number of seconds the
shell can be idle without receiving input. After the number of seconds
is reached, the shell exits. This security feature makes it less likely for
unattended shells to be accessed by unauthorized people. (This must
be set in the login shell for it actually to cause the shell to log out the
user.)|

### Exiting the shell
To exit the shell when you are finished, type exit or press Ctrl+D. If you go to the shell
from a Terminal window and you are using the original shell from that window, exiting
causes the Terminal window to close. If you are at a virtual console, the shell exits and
returns you to a login prompt.
