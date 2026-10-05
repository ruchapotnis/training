# Basic Linux Commands

| Command | Description |
| :--- | :--- |
| `whoami` | Current login name |
| `hostname` | Shows server name |
| `uname -r` | Kernel version |
| `uname -a` | Everything about OS and kernel |
| `pwd` | Present working directory |
| `ls` | List all the files and directories except hidden |
| `ls .` | List hidden files |
| `ls -a` | List all hidden as well as non-hidden files |
| `cd` | Change directory |
| `mkdir` | Make new directory |
| `touch` | Make new file |
| `cp <source> <destination>` | Copy |
| `mv <source> <destination>` | Move |
| `rm` | Remove files |
| `rm -rf` | Remove directories |
| `cat <file_name>` | Open file |
| `grep "spool" /etc/passwd` | Print only those lines that have "spool" in it |
| `sort` | Sort in ascending order |
| `sort -r` | Sort in descending order |
| `grep "spool" /etc/passwd \| cut -f 3 -d :` | Give 3rd column from all the lines containing "spool" and separated by ":" |
| `find` | Used to search for particular files (e.g., `find /etc -name "a*"` searches all files in `/etc` starting with 'a') |
| `useradd` | Add a new user account |
| `passwd` | Set/change password for a user |
| `ifconfig` | Used to check network configuration |

