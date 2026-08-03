In Red Hat Enterprise Linux 9 (RHEL 9), command-line completion (also called tab completion) is a powerful feature that speeds up typing, prevents syntax errors, and helps you discover available commands or arguments.
Here is how it works and how to use it.
- Core Mechanics
  - Single Tab: Pressing Tab once automatically fills in a unique command, file name, or variable name.
  - Double Tab: Pressing Tab twice displays a list of all available options if there are multiple matches.

### Types of Completion
- Commands: Type the first few letters of a command (e.g., syst) and press Tab to complete it to systemctl.
  - Paths and Files: Type a command followed by a partial path (e.g., cat /etc/res) and press Tab to complete it to cat /etc/resolv.conf.
  - Variables: Type $ followed by partial characters (e.g., echo $HO) and press Tab to complete environmental variables like $HOME.
  - Hostnames: Type SSH or Ping followed by a partial host found in your /etc/hosts file to auto-complete network destinations.
### Advanced Tab Completion (bash-completion)
RHEL 9 uses the bash-completion package to extend completion to command-specific options, flags, and arguments (e.g., auto-completing package names with dnf or service names with systemctl).
- Check status: It is usually installed by default in standard RHEL 9 environments.
- Manual Installation: If it is missing, install it using:
```bash
sudo dnf install bash-completion
```
Activation: The feature activates on your next login, or you can load it instantly in your current session by running:
```bash
source /etc/profile.d/bash_completion.sh
```
Practical Examples
Services: Type systemctl restart cr and press Tab to instantly complete the service name to crond.
- Packages: Type dnf install http and press Tab twice to see all available packages starting with "http".
- Network: Type nmcli connection up and press Tab to view a list of your configured network profiles.

## Interview Questions:-
- Q: If tab completion is completely broken for arguments but works for files, how do you troubleshoot it?
Answer: The core bash shell handles file path completion natively. If advanced argument completion (like completing service names) fails, the bash-completion package is either missing or its environment script hasn't been loaded.
Fix: Run rpm -q bash-completion to check if it is installed. If it is missing, run `sudo dnf install bash-completion`. If it is installed but inactive, run `source /etc/profile.d/bash_completion.sh` to reload it.

- Q: Where are the completion scripts managed in RHEL 9?
Answer: System-wide scripts provided by installed packages are located in /usr/share/bash-completion/completions/. Main configuration files and loader scripts reside in /etc/profile.d/bash_completion.sh.

- Q: Can you explain how to write a basic custom completion rule?
Answer: You use the built-in complete command in Bash. For example, to make a custom script named myscript only suggest directory names as arguments, you add this to your ~/.bashrc:
```bash
complete -d myscript
```
For complex arguments, you use `complete -F _function_name script_name` to point to a custom shell function that populates the COMPREPLY array variable.
