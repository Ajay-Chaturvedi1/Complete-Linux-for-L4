In a Linux administration interview, "command line editing" tests your speed, efficiency, and comfort level on the keyboard. Interviewers want to see that you do not manually backspace 50 times just to fix a typo at the beginning of a long command.
By default, RHEL 9 uses Emacs mode for command line editing inside the Bash shell. Here is the structured guide to shortcuts and configurations you must know for your interview.
##🚀 High-Frequency Shortcuts (The Essentials)
- When asked how you optimize your workflow on the CLI, group your answers by action types to show structured thinking.
  1. Cursor Movement (Stop using the Left/Right Arrow Keys)
     - Ctrl + A: Moves the cursor instantly to the beginning of the line.
     - Ctrl + E: Moves the cursor instantly to the end of the line (End).
     - Alt + F: Moves the cursor forward by one full word (Forward).
     - Alt + B: Moves the cursor backward by one full word (Backward).

  2. Cutting and Pasting Text (The "Kill Ring")In the Linux CLI, cutting is referred to as "killing" and pasting is referred to as "yanking".
     - Ctrl + K: Cuts all text from the cursor's current position to the end of the line.
     - Ctrl + U: Cuts all text from the cursor's current position back to the beginning of the line.
     - Ctrl + W: Cuts the single word immediately before the cursor.
     - Ctrl + Y: Pastes ("yanks") the last piece of text you cut using any of the shortcuts above.

  3. Quick Corrections
     - Ctrl + _ (or Ctrl + X then Ctrl + U): The CLI Undo command. It reverses your last editing change.
     - Alt + T: Swaps (transposes) the word the cursor is on with the word before it.
     - Ctrl + T: Swaps the character under the cursor with the character right before it (perfect for fixing typos like gmet instead of gtem).
  
  ### 🥇 Senior-Level Interview Questions & Configurations
  - Question 1: "I am a hardcore Vim user. I hate Emacs shortcuts. How can I use Vim keybindings to edit my command line in RHEL 9?"
    Answer: You can switch the Bash command line editing mode to Vi mode at any time by running the command: set -o vi.
    Once enabled, hitting Esc puts the command line into Vi command mode, allowing you to use standard Vim keys like 0 (start of line), $ (end of line), w (next word), and i (insert mode). To make this change permanent, add `set -o vi` to your `~/.bashrc`.
    > Note: To switch it back to default, use `set -o emacs`.
  - Question 2: "What is the fc command, and when is it superior to using standard shortcuts?"
    Answer: fc stands for "Fix Command". If you are typing a highly complex, multi-line loop or a massive configuration command and realize you made a syntax mistake, typing shortcuts on a single line becomes tedious.
    Running fc instantly opens your last attempted command inside your system's default text editor (like vi or nano). You can edit it freely with the full power of a text editor, save, and exit. The moment you close the editor, Bash executes the corrected command automatically.

  - Question 3: "How does the system know these shortcuts exist? What subsystem handles command line editing in RHEL 9?"
    Answer: Command line editing, shortcuts, and history searching are all handled by a specific shared library called `GNU Readline`. Readline reads its global configuration from `/etc/inputrc` and user-specific customizations from `~/.inputrc`.


 TABLE 3.3 Keystrokes for Cutting and Pasting Text from within
Command Lines

|Keystroke |Full Name| Meaning|
|-----------|-------|---------|
|Ctrl+K |Cut end of line | Cut text to the end of the line.|
|Ctrl+U |Cut beginning of line| Cut text to the beginning of the line.|
|Ctrl+W |Cut previous word |Cut the word located behind the cursor.|
|Alt+D |Cut next word| Cut the word following the cursor.|
|Ctrl+Y |Paste recent text |Paste most recently cut text.|
|Alt+Y |Paste earlier text |Rotate back to previously cut text and paste it.|
|Ctrl+C |Delete whole line |Delete the entire line. |  


TABLE 3.2 Keystrokes for Editing Command Lines
|Keystroke |Full Name |Meaning|
|-----------|----------|---------|
|Ctrl+D |Delete current| Delete the current character.|
|Backspace |Delete previous |Delete the previous character.|
|Ctrl+T |Transpose character |Switch positions of current and previous characters.|
|Alt+T |Transpose words |Switch positions of current and previous words.|
|Alt+U |Uppercase word |Change the current word to uppercase.|
|Alt+L |Lowercase word |Change the current word to lowercase.|
|Alt+C |Capitalize word |Change the current word to an initial capital.|
|Ctrl+V |Insert special character | Add a special character. For example, to add a Tab character, press Ctrl+V+Tab.|


TABLE 3.1 Keystrokes for Navigating Command Lines
|Keystroke| Full Name| Meaning|
|----------|-------|---------|
|Ctrl+F |Character forward |Go forward one character.|
|Ctrl+B |Character backward |Go backward one character.|
|Alt+F |Word forward| Go forward one word.|
|Alt+B |Word backward |Go backward one word.|
|Ctrl+A |Beginning of line| Go to the beginning of the current line.|
|Ctrl+E |End of line |Go to the end of the line.|
|Ctrl+L |Clear screen |Clear screen and leave line at the top of the screen.|

Question: "If your terminal hangs or freezes mid-typing and stops responding to standard editing shortcuts, what terminal flow control shortcut might have been accidentally triggered, and how do you unlock it?"Answer: The user likely hit Ctrl + S, which triggers XOFF flow control and freezes terminal output transmission. To unfreeze the terminal and resume editing, you must press Ctrl + Q (XON flow control).


Question: "How would you create a permanent, custom global shortcut key for all users on a RHEL 9 server—for example, making the F5 key clear the screen?"Answer: Command-line shortcuts are governed by the GNU Readline library. To make a global change, I would edit the file /etc/inputrc (or create a user-specific ~/.inputrc) and map the key sequence to the Readline function. For example: "\e[15~": clear-screen maps the F5 key.


