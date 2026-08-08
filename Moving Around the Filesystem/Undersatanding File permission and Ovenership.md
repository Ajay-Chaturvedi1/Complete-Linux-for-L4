> **Note**
> For a regular file, a dash appears in front of the nine-bit permissions indicator. Instead of a dash, you might see a d
> (for a directory), l (for a symbolic link), b (for a block device), c (for a character device), s (for a socket), or p (for a
> named pipe).


After you’ve worked with Linux for a while, you are almost sure to get a Permission
denied message. Permissions associated with files and directories in Linux were designed
to keep users from accessing other users’ private files and to protect important system files.
The nine bits assigned to each file for permissions define the access that you and others
have to your file. Permission bits for a regular file appear as -rwxrwxrwx. Those bits are
used to define who can read, write, or execute the file.

Of the nine-bit permissions, the first three bits apply to the owner’s permission, the next
three apply to the group assigned to the file, and the last three apply to all others. The r
stands for read, the w stands for write, and the x stands for execute permissions. If a dash
appears instead of the letter, it means that permission is turned off for that associated
read, write, or execute bit.
Because files and directories are different types of elements, read, write, and execute permissions
on files and directories mean different things. Table 4.2 explains what you can do
with each of them.
As noted earlier, you can see the permission for any file or directory by typing the ls -ld
command. The named file or directory appears as those shown in this example:
$ ls -ld ch3 test
-rw-rw-r-- 1 joe sales 4983 Jan 18 22:13 ch3
drwxr-xr-x 2 joe sales 1024 Jan 24 13:47 test
The first line shows that the ch3 file has read and write permission for the owner and the
group. All other users have read permission, which means that they can view the file but
cannot change its contents or remove it. The second line shows the test directory (indicated
by the letter d before the permission bits). The owner has read, write, and execute
permissions while the group and other users have only read and execute permissions. As a
result, the owner can add, change, or delete files in that directory, and everyone else can
only read the contents, change to that directory, and list the contents of the directory. (If
you had not used the -d options to ls, you would have listed files in the test directory
instead of permissions of that directory.)
Changing permissions with chmod (numbers)
If you own a file, you can use the chmod command to change the permission on it as you
please. In one method of doing this, each permission (read, write, and execute) is assigned
a number—r=4, w=2, and x=1—and you use each set’s total number to establish the
TABLE 4.2 Setting Read, Write, and Execute Permissions
Permission File Directory
Read View what’s
in the file.
See what files and subdirectories it contains.
Write Change the file’s
content, rename it,
or delete it.
Add files or subdirectories to the directory. Remove files or
directories from the directory.
Execute Run the file as
a program.
Change to the directory as the current directory, search
through the directory, or execute a program from the
directory. Access file metadata (file size, time stamps, and
so on) of files in that directory.
Chapter 4: Moving Around the Filesystem
107
4
permission. For example, to make permissions wide open for yourself as owner, you would
set the first number to 7 (4+2+1), and then you would give the group and others read-only
permission by setting both the second and third numbers to 4 (4+0+0), so that the final
number is 744. Any combination of permissions can result from 0 (no permission) through 7
(full permission).
Here are some examples of how to change permission on a file (named file) and what the
resulting permission would be:
The following chmod command results in this permission: rwxrwxrwx
# chmod 777 file
The following chmod command results in this permission: rwxr-xr-x
# chmod 755 file
The following chmod command results in this permission: rw-r--r--
# chmod 644 file
The following chmod command results in this permission: ---------
# chmod 000 file
The chmod command also can be used recursively. For example, suppose that you wanted
to give an entire directory structure 755 permission (rwxr-xr-x), starting at the $HOME/
myapps directory. To do that, you could use the -R option, as follows:
$ chmod -R 755 $HOME/myapps
All files and directories below, and including, the myapps directory in your home directory
will have 755 permissions set. Because the numbers approach to setting permission changes
all permission bits at once, it’s more common to use letters to change permission bits recursively
over a large set of files.
Changing permissions with chmod (letters)
You can also turn file permissions on and off using plus (+) and minus (–) signs, respectively,
along with letters to indicate what changes and for whom. Using letters, for each
file you can change permission for the user (u), group (g), other (o), and all users (a).
What you would change includes the read (r), write (w), and execute (x) bits. For example,
start with a file that has all permissions open (rwxrwxrwx). Run the following chmod
commands using minus sign options. The resulting permissions are shown to the right of
each command.
The following chmod command results in this permission: r-xr-xr-x
$ chmod a-w file
The following chmod command results in this permission: rwxrwxrw-
$ chmod o-x file
The following chmod command results in this permission: rwx------
Part II: Becoming a Linux Power User
108
$ chmod go-rwx file
Likewise, the following examples start with all permissions closed (---------). The plus
sign is used with chmod to turn permissions on.
The following chmod command results in this permission: rw-------
$ chmod u+rw files
The following chmod command results in this permission: --x--x--x
$ chmod a+x files
The following chmod command results in this permission: r-xr-x---
$ chmod ug+rx files
Using letters to change permission recursively with chmod generally works better than
using numbers because you can change bits selectively instead of changing all permission
bits at once. For example, suppose that you want to remove write permission for “other”
without changing any other permission bits on a set of files and directories. You could do
the following:
$ chmod -R o-w $HOME/myapps
This example recursively removes write permissions for “other” on any files and directories
below the myapps directory. If you had used numbers such as 644, execute permission
would be turned off for directories; using 755, execute permission would be turned on for
regular files. Using o-w, only one bit is turned off and all other bits are left alone.
Setting default file permission with umask
When you create a file as a regular user, it’s given permission rw-rw-r-- by default. A
directory is given the permission rwxrwxr-x. For the root user, file and directory permission
are rw-r--r-- and rwxr-xr-x, respectively. These default values are determined by
the value of umask. Enter umask to see what your umask value is. For example:
$ umask
0002
If you ignore the leading zero for the moment, the umask value masks what is considered
to be fully opened permissions for a file 666 or a directory 777. The umask value of 002
results in permission for a directory of 775 (rwxrwxr-x). That same umask results in a file
permission of 644 (rw-rw-r--). (Execute permissions are off by default for regular files.)
To change your umask value temporarily, run the umask command. Then try creating
some files and directories to see how the umask value affects how permissions are set.
For example:
$ umask 777 ; touch file01 ; mkdir dir01 ; ls -ld file01 dir01
d---------. 2 joe joe 6 Dec 19 11:03 dir01
----------. 1 joe joe 0 Dec 19 11:02 file01
$ umask 000 ; touch file02 ; mkdir dir02 ; ls -ld file02 dir02
Chapter 4: Moving Around the Filesystem
109
4
drwxrwxrwx. 2 joe joe 6 Dec 19 11:00 dir02/
-rw-rw-rw-. 1 joe joe 0 Dec 19 10:59 file02
$ umask 022 ; touch file03 ; mkdir dir03 ; ls -ld file03 dir03
drwxr-xr-x. 2 joe joe 6 Dec 19 11:07 dir03
-rw-r--r--. 1 joe joe 0 Dec 19 11:07 file03
If you want to change your umask value permanently, add a umask command to the
.bashrc file in your home directory (near the end of that file). The next time you open a
shell, your umask is set to whatever value you chose.
Changing file ownership
As a regular user, you cannot change ownership of files or directories to have them belong
to another user. You can change ownership as the root user. For example, suppose that you
created a file called memo.txt in the user joe’s home directory while you were root user.
Here’s how you could change it to be owned by joe:
# chown joe /home/joe/memo.txt
# ls -l /home/joe/memo.txt
-rw-r--r--. 1 joe root 0 Dec 19 11:23 /home/joe/memo.txt
Notice that the chown command changed the user to joe but left the group as root. To
change both user and group to joe, you could enter the following instead:
# chown joe:joe /home/joe/memo.txt
# ls -l /home/joe/memo.txt
-rw-r--r--. 1 joe joe 0 Dec 19 11:23 /home/joe/memo.txt
The chown command can be use recursively as well. Using the recursive option (-R) is helpful
if you need to change a whole directory structure to ownership by a particular user. For
example, if you inserted a USB drive, which is mounted on the /media/myusb directory,
and you wanted to give full ownership of the contents of that drive to the user joe, you
could enter the following:
# chown -R joe:joe /media/myusb
