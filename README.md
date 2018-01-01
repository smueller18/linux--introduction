# Linux Introduction

This content is a summary of the official "Linux Introduction" course from the Linux Foundation provided by [edx.org](https://courses.edx.org/courses/course-v1:LinuxFoundationX+LFS101x+1T2017/course/).

The commands are restricted to the Ubuntu distribution.


## Command Line

### Switch between virtual terminals (VT 1 - VT 6) with `CTRL-ALT-Fx` where `x` is from 1 to 6. VT 7 is reserved for the GUI.

### Start and stop the desktop manager
```
sudo systemctl start gdm
sudo systemctl stop gdm
```

### SSH (Secure Shell)
`ssh username@remote-server.com`

### Shutdown
| Command | Result |
| - | - |
| `halt`, `poweroff` or `shutdown -h` | halt |
| `reboot` or `shutdown -r` | reboot |

Planned shutdown with notification: `sudo shutdown -h 10:00 "Shutdown Message"`

Immidiately shutdown: `shutdown -h now`

### Locate Programs
| Command | Result |
| - | - |
| `which` | prints out where the diff program resides exactly |
| `whereis` | prints also the locating source and man files |

### Wildcards
| Wildcard | Result |
| - | - |
| ? | Matches any single character |
| * | Matches any string of characters |
| [set] | Matches any charackter in the set of characters, for example [adf] will match any ocurrence of "a", "d" or "f" |
| [!set] | Matches any character not in the set of characters |


### File and directory commands
| Command | Result | Example | Hint |
| - | - | - | - |
| `mv` | renames a file/directory |  |  |
| `rm` | removes file/directory |  |  |
| `rm -f` | Forcefully removes a file/directory |  |  |
| `rm -rf` | forcefully remove a directory recursively |  |  |
| `rm -i` | Interactively removes a file/directory |  |  |
| `ls` | List the contents of the present working directory |  |  |
| `ls -a` | List the contents including hidden files |  |  |
| `ls -l` | Use long listing format |  |  |
| `ls -h` | Print human readable file sizes |  |  |
| `ls -R` | List the contents recursivly |  |  |
| `tree` | Displays a tree view |  |  |
| `locate` | Searches through database of files and directories which is created by the command `updatedb` |  |  |
| `ln` | creates hard link |  |  |
| `ln -s` | creates soft link | `ln -s <TARGET> <LINK_NAME>` |  |
| `find -name` | find in files/directories | `find /var/log -name "*.log"` |  |
| `find -iname` | find non case sensitive in files/directories | `find /var/log -iname "*.log"` |  |
| `find [-ctime or -time or -mtime]` | find files/directories by date metadata | `find / -ctime 3` | ctime changed ownership/permission, a accessed/last read, m modified/last written |
| `find -size` | find files/directories by size | `find / -size +10M` | + for greater, - for less |
| `find -type [d or l or f]` | find only selected types (d directory, l symbolic link, f file) | `find /var/log -type f "*.log"` |  |
| `find -name * -exec <COMMAND> {} ’;’` | find files and run commands on them | find -name "*.swp" -exec rm {} ’;’ | {} is placeholder for all matched files |


### Directory commands
| Command | Result |
| - | - |
| `pwd` | displays present working directory |
| `cd ~` or `cd` or `cd $HOME` | Change to the home directory |
| `cd ..` | Change to parent directory |
| `cd -` | Change to previous directory |
| `cd /` | Change to the root directory |
| `pushd` | changes the directory and stores the recent directory to a list |
| `popd` | sends you back to the most recent directory stored with pushd |
| `mkdir` | creates dir |
| `rmdir` | removes an empty directory |

### File commands
| `touch` | create emtpy file | `-t` allows to set time stamp |
| - | - | - |
| `cat` | views complete file(s) |  |
| `tac` | view complete file(s) backwards |  |
| `less` | view complete file in scroll view and offers search | use `/` to search pattern in forward direction and `?` backwards, `q` to quit |
| `tail` | prints last lines of a file | `tail -15`, `tail -n15`, `tail -n 15` |
| `head` | prints first lines of a file |  |

### File streams
| Name | Symbolic Name | Value | Example |
| - | - | - | - |
| standard input | stdin | 0 | keyboard |
| standard output | stdout | 1 | terminal |
| standard error | stderr | 2 | logfile |


| Command | Description |
| - | - |
| `do_something < input-file` | Input data from file |
| `do_something > output-file` | Output stdout to file |
| `do_something 2> error-file` | Output stderr to file |
| `do_something > all-output-file 2>&1` | Output stdout and stderr to file |
| `do_something >& all-output-file` | Easier syntax for bash, outputs stdout and stderr to file |

### Pipes
Use to redirect output from one command to the input of another command
```
$ command1 | command2 | command3
```

### Manual
@TODO
- man
- info
- --help
- `/usr/share/doc`

### Package Management
| Command | Result | Hint |
| - | - | - |
| apt install | install package |  |
| apt search |  |  |
| add-apt-repository |  |  |
| add-apt-key |  |  |

### Processes
| Command | Result | Example | Hint |
| - | - | - | - |
| `ps` | show processes |  |  |
| `ps -u` | show processes of a specified user |  |  |
| `ps -ef` | show all processes in full detail |  |  |
| `ps -eLf` | show processes |  |  |
| `ps aux` | show processes with usage of CPU and memory |  |  |
| `pstree` | shows processes in form of a tree view |  |  |
| `top` | shows processes interactively |  |  |
| `htop` | shows processes interactively advanced |  |  |
| `kill` |  | kill -9 <PID> |  |
| `sleep` | pause running process | `sleep 100` |  |
| `bg` | run stopped command in background | `bg 2`, run second job |  |
| `fg` | run stopped command in foreground |  |  |
| `jobs` | show jobs running in background | + is next job, - second job running by `bg` or `fg` | `-l` shows pid |
| `at` | run command in future | `at now + 1 minutes` | after typing command press `CTRL-D` |
| `CTRL-C` | interrupt foreground job |  |  |
| `CTRL-Z` | suspend foreground job |  |  |
| `<COMMAND> &` | run process in background |  |  |


> The priority for a process can be set by specifying a nice value, or niceness, for the process. The lower the nice value, the higher the priority. Low values are assigned to important processes, while high values are assigned to processes that can wait longer. A process with a high nice value simply allows other processes to be executed first. In Linux, a nice value of -20 represents the highest priority and 19 represents the lowest. (This does sound kind of backwards, but this convention, the nicer the process, the lower the priority, goes back to the earliest days of UNIX.)

#### Load average
> Load average is the average of the load number for a given period of time. It takes into account processes that are:
- Actively running on a CPU.
- Considered runnable, but waiting for a CPU to become available.
- Sleeping: i.e., waiting for some kind of resource (typically, I/O) to become available.

The load average can be viewed by running `w`, `top` or `uptime`

### Cron
Set cron jobs with `crontab -e`. Each line contains 6 fields:

| Field | Description | Values |
| - | - | - |
| MIN | minutes | 0 to 59 |
| HOUR | Hour field | 0 to 23 |
| DOM | Doay of Month | 1-31 |
| MON | Month field | 1-12 |
| DOW | Day of Week | 0-6 (0 = Sunday) |
| CMD | Command | Any command to be executed |

Example
- `* * * * * /usr/bin/script.sh`, execution every minute of every hour of every day of the month, and every month and every day in week
- `30 08 10 06 * /usr/bin/script.sh`, execution at 8.30am, 10-June, irrespective of the day of the week

## Filesystems
@TODO
