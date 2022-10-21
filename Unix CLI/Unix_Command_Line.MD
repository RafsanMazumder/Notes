# Process
## *init* 
* When a system starts, the kernel launces init script, which starts all the system processes. 
* PID: 1
## PID
* The kernel maintains information about each process by assigning a number called process ID (PID).
## Viewing Processes
### *ps*
| PID    | TTY      | TIME    | CMD  |
| ------ | -------- | ------- | ---- |
| 23137  | ttys000  | 0:00.59 | -zsh |
* Provides a snapshot of the machine processes.
* TTY: Short for "teletype", the controlling terminal for the processs
* TIME: The cumulative CPU time of the process, shown in minutes and seconds
* CMD: The name of the command that starts the process

### *ps aux*
* **a** show process stats
* **u** show process's user
* **x** show processes not attached to terminal

| USER    | PID   | %CPU  | %MEM | VSZ      | RSS    | TT | STAT | STARTED | TIME    | COMMAND          | 
| -       | -     | -     | -    | -        | -      | -  | -    | -       | -       | -                |
| rafsan  | 23127 | 13.5  | 0.4  | 36126520 | 127460 | ?? | S    | Thu12PM | 2:18.27 | /usr/libexec/dmd |

* **%CPU** The CPU uitilization of the process
* **%MEM** The percentage of the process's resident set size (RSS) to the physical memory on the machine
* **VSZ** Virtual memory size (kilobytes)
* **RSS** Resident set size (kilobytes)
* **STAT** The process's state code

#### Difference between DSZ & RSS
##### RSS (Resident Set Size)
* How much RAM memory that is allocated to the process
* Does not include memory that is swapped out
* Does include memory from shared libraries as long as the pages from these libraries are actually in memory

##### VSZ (Virtual Memory Size)
* All memory that the process can access, including memory that is swapped out, memory allocated but not used, and memory from shared libraries. 

| Type             | Total Memory | RAM Memory  |
| -                | -            | -           |
| binary           | 500K         | 400K        |
| shared libraries | 2500K        | 1000K       | 
| steak/heap       | 200K         | 100K        |
|                  | 3200K (RSS)  | 1500K (VSZ) |

