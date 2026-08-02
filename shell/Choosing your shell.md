In most Linux systems, your default shell is the bash shell. To find out what is your default
login shell, enter the following commands:
```bash 
$ who am i
chris pts/0 2019-10-21 22:45 (:0.0)
$ grep chris /etc/passwd
chris:x:13597:13597:Chris Negus:/home/chris:/bin/bash
```
You can see information about your current login session by using the who command. In
the following example, the -u option says to add information about idle time and the process
ID and -H asks that a header be printed:
```bash
$ who -uH
NAME LINE TIME IDLE PID COMMENT
chris tty1 Jan 13 20:57 . 2019
```
The output from this who command shows that the user chris is logged in on tty1
(which is the first virtual console on the monitor connected to the computer) and his login
session began at 20:57 on January 13. The IDLE time shows how long the shell has been
open without any command being typed (the dot indicates that it is currently active).



In an interview setting, the phrase "choosing your shell" usually transitions the conversation from basic system console navigation to how a user or administrator interacts with the operating system once logged in.
In RHEL 9, the default login shell is Bash (Bourne Again Shell), but interviewers often test your knowledge on how shells are managed, changed, and configured across the enterprise.
###🥉 Junior Level Questions: Shell Basics
- How do you find out which shell you are currently using?
Answer: Run `echo $SHELL` to see your default login shell, or run `ps -p $$` to see the currently running shell process.
- Where is the user's default shell configuration stored permanently?
Answer: In the `/etc/passwd` file. The last field of each user's line specifies their login shell (e.g., /bin/bash).
- What is a non-login shell, and what is its default path?
Answer: A non-login shell (like `/sbin/nologin` or `/bin/false`) prevents a service account or system user from logging into an interactive terminal session while still allowing system processes to run under that account.

###🥈 Mid-Level Questions: Shell Management
- How do you safely change a user's default login shell in RHEL 9?
Answer: Use the chsh (change shell) command or `usermod -s /path/to/shell username`.
- Where does the system look to verify if a shell is safe and valid before letting a user switch to it?
Answer: The /etc/shells file. If a shell is not listed in this file, the chsh command will reject it by default for security reasons.
- What is the difference between .bash_profile and .bashrc?
Answer: .bash_profile executes only once during a login shell session (perfect for environment variables).
> .bashrc executes every time a new interactive non-login shell or terminal window is opened (perfect for aliases and functions).

### 🥇 Senior Level Questions: Enterprise Shell Security & Customization
- If you need to apply a custom alias or environment variable globally to every single Bash user upon login, where should you configure it?
Answer: Drop a custom script ending in .sh inside the /etc/profile.d/ directory. It is cleaner and safer than modifying /etc/profile directly.
- How do you configure a specific user account so that it can only execute a highly restricted subset of commands?
Answer: Assign them the Restricted Bash shell (/bin/rbash). It prevents them from changing directories (cd), modifying $PATH, or executing commands containing slashes (/).
- What happens to standard environment variables when a system administrator switches users using su username versus su - username?
Answer: Running su username keeps the current user's environment. Running su - username (or su -l) simulates a completely fresh login shell, clearing old variables and loading the target user's specific profile configuration.

## what is no login shell and why we use it?

In RHEL 9 and other Linux distributions, a no-login shell is a special configuration assigned to a user account that prevents a person from logging into the system interactively.
Instead of an actual command interpreter (like /bin/bash), the user is assigned a dummy shell binary—most commonly /sbin/nologin or /bin/false.
Here is how to explain this concept and its use cases to an interviewer.
### 🛡️ The Two Types of No-Login Shells
When an interviewer asks about this, you should demonstrate that you know the difference between the two primary binaries used:
- /sbin/nologin: When someone attempts to log in (via SSH, GUI, or Virtual Console), the system denies entry and politely displays a message: "This account is currently not available."
- /bin/false: This is a more abrupt restriction. It simply terminates the login attempt immediately and returns an exit code of 1 (false) without displaying any message.

### ⚙️ Why We Use It (Enterprise Use Cases)
In a corporate environment, security is based on the Principle of Least Privilege. You must explain that many accounts on a Linux server exist solely to run specific background processes, not for human beings to log into.
1. System and Service Accounts
Applications like web servers (Apache/Nginx), databases (MySQL/PostgreSQL), and mail servers (Postfix) need a designated user account to own their files and run their daemons safely.
- Example: The apache user needs access to files in /var/www/html/, but no human should ever log in as the apache user. Assigning it `/sbin/nologin` keeps the service running while closing a massive security loophole.
2. FTP, Mail, or Samba-Only Users
Sometimes you create users who only need to upload files via SFTP or access a network share via Samba.
- Example: A client needs to upload logs via SFTP. They need an account to authenticate, but they do not need a command line to browse the server.
3. Temporary Account Suspension
  If an employee leaves the company or a contractor's access expires, you might want to freeze their account without deleting their files immediately.
- Example: Running usermod -s /sbin/nologin username instantly revokes their ability to log in while keeping their data intact for auditing.

### 💻 Interviewer Check: "Can a no-login user still run commands?"
- A favorite trick question for senior-level interviewers is: "If a user has /sbin/nologin as their shell, can they still execute a process or script?"
The Answer: Yes. They cannot log in interactively, but a system administrator (root) can still force a command to run under that user's identity using the -s (shell) flag with su or sudo.
The Command:
```bash
sudo -u apache -s /bin/bash /opt/backup_script.sh
```
This runs the script securely as the apache user, even though apache cannot log in on its own

### Additional commands:
```bash
$ uname
Linux
$ uname -a
Linux mydesktop 5.3.7-301.fc31.x86_64 #1 SMP Mon Oct 21 19:18:58 UTC
2019 x86_64 x86_64 x86_64 GNU/Linux
$ date
Wed 04 Mar 2020 09:06:25 PM EST
$ date +'%d/%m/%y'
04/03/20
$ date +'%A, %B %d, %Y'
Wednesday, March 04, 2020
```
To find out information about your identity, use the id command as follows:
```bash 
$ id
uid=1000(chris) gid=1000(chris) groups=1005(sales), 7(lp)
```

