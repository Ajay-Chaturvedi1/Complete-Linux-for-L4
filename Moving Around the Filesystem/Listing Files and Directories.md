<img width="739" height="274" alt="image" src="https://github.com/user-attachments/assets/c02c0ec2-7b61-43b7-81a8-72a04e079554" />
Displaying a long list (-l option) of the contents of your home directory shows you more
about file sizes and directories. The total line shows the total amount of disk space used
by the files in the list (158 kilobytes in this example). Adding the all files option (-a) displays
files that begin with a dot (.). Directories such as the current directory (.) and the
parent directory (..)—the directory above the current directory—are noted as directories
by the letter d at the beginning of each entry. Each directory begins with a d and each file
begins with a dash (-).
The file and directory names are shown in column 7. In this example, a dot (.) represents /
home/joe and two dots (..) represent /home—the parent directory of /joe. Most of the
files in this example are dot (.) files that are used to store GUI properties (.kde directory)
or shell properties (.bash files). The only non-dot file in this list is the one named letter.
Column 3 shows the directory or file owner. The /home directory is owned by root, and
everything else is owned by the user joe, who belongs to the sales group (groups are listed
in column 4).
In addition to the d or -, column 1 on each line contains the permissions set for that file
or directory. Other information in the listing includes the number of hard links to the item
(column 2), the size of each file in bytes (column 5), and the date and time each file was
most recently modified (column 6).

### Here are a few other facts about file and directory listings:
- ■■ The number of characters shown for a directory (4096 bytes in these examples)
reflects the size of the file containing information about the directory. Although
this number can grow above 4096 bytes for a directory that contains lots of files,
this number doesn’t reflect the size of files contained in that directory.
- ■■ The format of the time and date column can vary. Instead of displaying “May 12,”
the date might be displayed as “2019-05-12,” depending upon the distribution
and the language setting (LANG variable).
- ■■ On occasion, instead of seeing the execute bit (x) set on an executable file, you
may see an s in that spot instead. With an s appearing within either the owner
(-rwsr-xr-x) or group (-rwxr-sr-x) permissions, or both (-rwsr-sr-x), the
application can be run by any user, but ownership of the running process is
assigned to the application’s user/group instead of that of the user launching the
command. This is referred to as a set UID or set GID program, respectively. For
example, the mount command has permissions set as -rwsr-xr-x. This allows
any user to run mount to list mounted filesystems (although you still have to
be root to use mount to actually mount filesystems from the command line, in
most cases).
- ■■ If a t appears at the end of a directory, it indicates that the sticky bit is set for
that directory (for example, drwxrwxr-t). By setting the sticky bit on a directory,
the directory’s owner can allow other users and groups to add files to the
directory but prevent users from deleting each other’s files in that directory.
With a set GID assigned to a directory, any files created in that directory are
assigned the same group as the directory’s group. (If you see a capital S or T
instead of the execute bits on a directory, it means that the set GID or sticky bit
permission, respectively, was set, but for some reason the execute bit was not
also turned on.)
- ■■ If you see a plus sign at the end of the permission bits (for example, -rw-rwr--+),
it means that extended attributes (+), such as Access Control Lists (ACLs),
are set on the file. A dot at the end (.) indicates that SELinux is set on the file.

- The -t option displays files in the order in which they were most recently modified. With the -F option, a backslash (/) appears at the end of directory names, an asterisk (*) is added to executable files, and an at sign (@) is shown next to symbolic links. To show hidden and non-hidden files:
```bash
$ ls -a
. apple docs grapefruit pointer_to_apple .stuff watermelon
.. banana grape .hiddendir script.sh .tmpfile
```
To list all files by time most recently modified:
```bash
$ ls -at
.tmpfile .hiddendir .. docs watermelon banana script.sh
. .stuff pointer_to_apple grapefruit apple grape
```
To list files and append file-type indicators:
```bash
$ ls -F
apple banana docs/ grape grapefruit pointer_to_apple@ script.sh*
watermelon
```
To avoid displaying certain files or directories when you use ls, use the --hide= option.
In the next set of examples, any file beginning with g does not appear in the output. Using
a -d option on a directory shows information about that directory instead of showing
the files and directories the directory contains. The -R option lists all files in the current
directory as well as any files or directories that are associated with the original directory.
The -S option lists files by size.
To exclude any files beginning with the letter g in the list:
```bash
$ ls --hide=g*
apple banana docs pointer_to_apple script.sh watermelon
```
To list info about a directory instead of the files it contains:
```bash
$ ls -ld $HOME/test/
drwxrwxr-x. 4 joe joe 4096 Dec 18 22:00 /home/joe/test/
```
To create multiple directory layers (-p is needed):
```bash
$ mkdir -p $HOME/test/documents/memos/
```
To list all files and directories recursively from current directory down:
```bash
$ ls -R
```

To list files by size:
```bash
$ ls -S
```
