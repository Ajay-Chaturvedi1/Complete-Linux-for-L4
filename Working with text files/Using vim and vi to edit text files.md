It’s almost impossible to use Linux for any period of time and not need a text editor because, as
noted earlier, most Linux configuration files are plain-text files that you will almost certainly need
to change manually at some point.
If you are using a GNOME desktop, you can run gedit (type gedit into the Search box and press
Enter, or select Applications ➪ Accessories ➪ gedit), which is fairly intuitive for editing text.

### Adding text
To get into input mode, type an input command letter. To begin, type any of the following
letters. When you are finished inputting text, press the Esc key (sometimes twice) to return
to command mode. Remember the Esc key!
a: The add command. With this command, you can input text that starts to the right of
the cursor.
A: The add at end command. With this command, you can input text starting at the
end of the current line.
i: The insert command. With this command, you can input text that starts to the left
of the cursor.
I: The insert at beginning command. With this command, you can input text that starts
at the beginning of the current line.
o: The open below command. This command opens a line below the current line and
puts you in insert mode.
O: The open above command. This command opens a line above the current line and
puts you in insert mode.

Tip
When you are in insert mode, -- INSERT -- appears at the bottom of the screen.

Type a few words, and press Enter. Repeat that a few times until you have a few lines of
text. When you’re finished typing, press Esc to return to command mode. Now that you
have a file with some text in it, try moving around in your text with the keys or letters
described in the next section.

Tip
Remember the Esc key! It always places you back into command mode. Remember that sometimes you must press
Esc twice. For example, if you type a colon (:) to go into ex mode, you must press Esc twice to return to command
mode.

### Moving around in the text
To move around in the text, you can use the up, down, right, and left arrows. However, many of
the keys for moving around are right under your fingertips when they are in typing position:
Arrow keys: Move the cursor up, down, left, or right in the file one character at a time.
To move left and right, you can also use Backspace and the spacebar, respectively.
If you prefer to keep your fingers on the keyboard, move the cursor with h (left), l
(right), j (down), or k (up).
w: Moves the cursor to the beginning of the next word (delimited by spaces, tabs, or
punctuation).
W: Moves the cursor to the beginning of the next word (delimited by spaces or tabs).
b: Moves the cursor to the beginning of the previous word (delimited by spaces, tabs,
or punctuation).
B: Moves the cursor to the beginning of the previous word (delimited by
spaces or tabs).
0 (zero): Moves the cursor to the beginning of the current line.
$: Moves the cursor to the end of the current line.
H: Moves the cursor to the upper-left corner of the screen (first line on the screen).

M: Moves the cursor to the first character of the middle line on the screen.
L: Moves the cursor to the lower-left corner of the screen (last line on the screen).

### Deleting, copying, and changing text
The only other editing that you need to know is how to delete, copy, or change text. The
x, d, y, and c commands can be used to delete and change text. These can be used along
with movement keys (arrows, PgUp, PgDn, letters, and special keys) and numbers to indicate
exactly what you are deleting, copying, or changing. Consider the following examples:
x: Deletes the character under the cursor.
X: Deletes the character directly before the cursor.
d<?>: Deletes some text.
c<?>: Changes some text.
y<?>: Yanks (copies) some text.
The <?> after each letter in the preceding list identifies the place where you can use a
### movement command to choose what you are deleting, changing, or yanking. For example:
dw: Deletes (d) a word (w) after the current cursor position.
db: Deletes (d) a word (b) before the current cursor position.
dd: Deletes (d) the entire current line (d).
c$: Changes (c) the characters (actually erases them) from the current character to the
end of the current line ($) and goes into input mode.
c0: Changes (c) (again, erases) characters from the previous character to the beginning
of the current line (0) and goes into input mode.
cl: Erases (c) the current letter (l) and goes into input mode.
cc: Erases (c) the line (c) and goes into input mode.
yy: Copies (y) the current line (y) into the buffer.
y): Copies (y) the current sentence ( ) ), to the right of the cursor, into the buffer.
y}: Copies (y) the current paragraph ( } ), to the right of the cursor, into the buffer.

### Any of the commands just shown can be further modified using numbers, as you can see in the following examples:
3dd: Deletes (d) three (3) lines (d), beginning at the current line.
3dw: Deletes (d) the next three (3) words (w).
5cl: Changes (c) the next five (5) letters (l) (that is, removes the letters and enters
input mode).
12j: Moves down (j) 12 lines (12).
5cw: Erases (c) the next five (5) words (w) and goes into input mode.
4y): Copies (y) the next four (4) sentences ( ) ).

### Pasting (putting) text
After text has been copied to the buffer (by deleting, changing, or yanking it), you can
place that text back in your file using the letter p or P. With both commands, the text most
recently stored in the buffer is put into the file in different ways.
P: Puts the copied text to the left of the cursor if the text consists of letters or words;
puts the copied text above the current line if the copied text contains lines of text.
p: Puts the buffered text to the right of the cursor if the text consists of letters or
words; puts the buffered text below the current line if the buffered text contains
lines of text.
Repeating commands
After you delete, change, or paste text, you can repeat that action by typing a period (.).
For example, with the cursor on the beginning of the name Joe, you type cw and then
type Jim to change Joe to Jim. You search for the next occurrence of Joe in the file,
position the cursor at the beginning of that name, and press a period. The word changes to
Jim, and you can search for the next occurrence. You can go through a file this way, pressing
n to go to the next occurrence and period (.) to change the word.
Exiting vi
To wrap things up, use the following commands to save or quit the file:
ZZ: Saves the current changes to the file and exits from vi.
:w: Saves the current file, but you can continue editing.
:wq: Works the same as ZZ.
:q: Quits the current file. This works only if you don’t have any unsaved changes.
:q!: Quits the current file and doesn’t save the changes you just made to the file.


Tip
If you’ve really trashed the file by mistake, the :q! command is the best way to exit and abandon your changes. The
file reverts to the most recently changed version. So, if you just saved with :w, you are stuck with the changes up
to that point. However, despite having saved the file, you can type u to back out of changes (all the way back to the
beginning of the editing session if you like) and then save again.


You have learned a few vi editing commands. I describe more commands in the following
sections. First, however, consider the following tips to smooth out your first trials with vi:
Esc: Remember that Esc gets you back to command mode. (I’ve watched people press
every key on the keyboard trying to get out of a file.) Esc followed by ZZ gets you
out of command mode, saves the file, and exits.
u: Press u to undo the previous change you made. Continue to press u to undo the
change before that and the one before that.


Ctrl+R: If you decide that you didn’t want to undo the previous undo command, use
Ctrl+R for Redo. Essentially, this command undoes your undo.
Caps Lock: Beware of hitting Caps Lock by mistake. Everything that you type in vi
has a different meaning when the letters are capitalized. You don’t get a warning
that you are typing capitals; things just start acting weird.
:!command: You can run a shell command while you are in vi using :! followed by a
shell command name. For example, type :!date to see the current date and time,
type :!pwd to see what your current directory is, or type :!jobs to see whether
you have any jobs running in the background. When the command completes, press
Enter and you are back to editing the file. You could even use this technique to
launch a shell (:!bash) from vi, run a few commands from that shell, and then
type exit to return to vi. (I recommend doing a save before escaping to the shell,
just in case you forget to go back to vi.)
Ctrl+g: If you forget what you are editing, pressing these keys displays the name of the
file that you are editing and the current line that you are on at the bottom of the
screen. It also displays the total number of lines in the file, the percentage of how
far you are through the file, and the column number the cursor is on. This just helps
you get your bearings after you’ve stopped for a cup of coffee at 3 a.m.


Skipping around in the file
Besides the few movement commands described earlier, there are other ways of moving
around a vi file. To try these out, open a large file that you can’t damage too much. (Try
copying /var/log/messages to /tmp and opening it in vi.) Here are some movement
commands that you can use:
Ctrl+f: Pages ahead one page at a time.
Ctrl+b: Pages back one page at a time.
Ctrl+d: Pages ahead one-half page at a time.
Ctrl+u: Pages back one-half page at a time.
G: Goes to the last line of the file.
1G: Goes to the first line of the file.
35G: Goes to any line number (35, in this case).


Searching for text
To search for the next or previous occurrence of text in the file, use either the slash (/) or
the question mark (?) character. Follow the slash or question mark with a pattern (string of
text) to search forward or backward, respectively, for that pattern. Within the search, you
can also use metacharacters. Here are some examples:
/hello: Searches forward for the word hello.
?goodbye: Searches backward for the word goodbye.
/The.*foot: Searches forward for a line that has the word The in it and also, after
that at some point, the word foot.
?[pP]rint: Searches backward for either print or Print. Remember that case matters
in Linux, so make use of brackets to search for words that could have different
capitalization.
After you have entered a search term, simply type n or N to search again in the same direction
(n) or the opposite direction (N) for the term.

Using ex mode
The vi editor was originally based on the ex editor, which didn’t let you work in fullscreen
mode. However, it did enable you to run commands that let you find and change
text on one or more lines at a time. When you type a colon and the cursor goes to the bottom
of the screen, you are essentially in ex mode. The following are examples of some of
those ex commands for searching for and changing text. (I chose the words Local and
Remote to search for, but you can use any appropriate words.)
:g/Local: Searches for the word Local and prints every occurrence of that
line from the file. (If there is more than a screenful, the output is piped to the
more command.)
:s/Local/Remote: Substitutes Remote for the first occurrence of the word Local
on the current line.
:g/Local/s//Remote: Substitutes the first occurrence of the word Local on every
line of the file with the word Remote.
:g/Local/s//Remote/g: Substitutes every occurrence of the word Local with the
word Remote in the entire file.
:g/Local/s//Remote/gp: Substitutes every occurrence of the word Local with the
word Remote in the entire file and then prints each line so that you can see the
changes (piping it through less if output fills more than one page).

> ### Learning more about vi and vim
> To learn more about the vi editor, try typing vimtutor. The vimtutor command opens a
> tutorial in the vim editor that steps you through common commands and features you can
> use in vim. To use vimtutor, install the vim-enhanced package.
































