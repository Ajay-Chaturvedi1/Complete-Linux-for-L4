Commands for moving, copying, and deleting files are fairly straightforward. To change
the location of a file, use the mv command. To copy a file from one location to another, use
the cp command. To remove a file, use the rm command. These commands can be used to
act on individual files and directories or recursively to act on many files and directories at
once. Here are some examples:
$ mv abc def
$ mv abc ~
$ mv /home/joe/mymemos/ /home/joe/Documents/
The first mv command moves the file abc to the file def in the same directory (essentially
renaming it), whereas the second mv command moves the file abc to your home directory

(~). The next mv command moves the mymemos directory (and all its contents) to the /
home/joe/Documents directory.
By default, the mv command overwrites any existing files if the file to which you are
moving exists. However, many Linux systems alias the mv command so that it uses the -i
option (which causes mv to prompt you before overwriting existing files). Here’s how to
check if that is true on your system:
$ alias mv
alias mv='mv -i'
Here are some examples of using the cp command to copy files from one location
to another:
$ cp abc def
$ cp abc ~
$ cp -r /usr/share/doc/bash-completion* /tmp/a/
$ cp -ra /usr/share/doc/bash-completion* /tmp/b/

Copying directories from one location to other
```bash
# cp –rvfp <dir name> <destination name>
#cp –rvfp mydir2 mydir
```
The first copy command (cp) copies abc to the new name def in the same directory,
whereas the second copies abc to your home directory (~), keeping the name abc. The two
recursive (-r) copies copy the bash-completion directory and all of the files it contains,
first to new /tmp/a/ and /tmp/b/ directories. If you run ls -l on those two directories,
you see that for the cp command run with the archive (-a) option, the date/time stamps
and permissions are maintained by the copy. Without the -a, current date/time stamps are
used, and permissions are determined by your umask.
The cp command typically also is aliased with the -i option in order to prevent you from
inadvertently overwriting files.
As with the cp and mv commands, rm is also usually aliased to include the -i option. This
can prevent the damage that can come from an inadvertent recursive remove (-r) option.
Here are some examples of the rm command:
$ rm abc
$ rm *
The first remove command deletes the abc file; the second removes all of the files in the
current directory (except that it doesn’t remove directories and/or any files that start
with a dot). If you want to remove a directory, you need to use the recursive (-r) option
to rm or, for an empty directory, you can use the rmdir command. Consider the following
examples:
$ rmdir /home/joe/nothing/
$ rm -r /home/joe/bigdir/
$ rm -rf /home/joe/hugedir/
The rmdir command in the preceding code only removes the directory (nothing) if it is
empty. The rm -r example removes the directory bigdir and all of its contents (files and
multiple levels of subdirectories), but it prompts you before each is removed. When you
add the force option (-f), the hugedir directory and all of its contents are immediately
removed, without prompting.

Caution
When you override the -i option on the mv, cp, and rm commands, you risk removing some (or lots) of files by mistake.
Using wildcards (such as *) and no -i makes mistakes even more likely. That said, sometimes you don’t want
to be bothered to step through each file you delete. You have other options as follows:
■■ As noted with the -f option, you can force rm to delete without prompting. An alternative is to run rm,
cp, or mv with a backslash in front of it (\rm bigdir). The backslash causes any command to run unaliased.
■■ Another alternative with mv is to use the -b option. With -b, if a file of the same name exists at the destination,
a backup copy of the old file is made before the new file is moved there.

# Table 
Command	Primary Function	Key L4-Level Options & Considerations 
cp	Copy files or directories.	-p (preserve attributes), -a (archive mode, for recursive copies), -u (update, copy only when source is newer). Critical for backup and replication tasks.
mv	Move (or rename) files/directories.	-i (interactive, prompts before overwrite), -f (force, no prompt), -u (update, move only if newer).
rm	Remove (delete) files/directories.	-r (recursive, mandatory for directories), -f (force, suppress prompts), -i (interactive). Always used with extreme caution.
