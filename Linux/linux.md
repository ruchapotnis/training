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

# Linux File System 

When Linux is installed on your server, these standard directories and system files are created by default.

## Core Directories

| Directory | Description |
| :--- | :--- |
| `/` | **Root directory**. The starting point of the entire Linux file system hierarchy. All paths begin here. |
| `/boot` | Contains all the critical **bootloader files** required to start the operating system. |
| `/dev` | Contains **device driver files** for hardware. Serves as the link between the OS and physical devices. |
| `/home` | The default **home directory** for all local, non-root system users. |
| `/root` | The dedicated **home directory** exclusively for the root (administrator) user. |
| `/lib` | Contains essential **shared library files** and kernel modules needed for system booting. |
| `/var` | Stores **variable data**, including system, hardware, and application log files. |
| `/proc` | A virtual file system serving as a **mount point to RAM** to monitor ongoing processes and hardware status. |
| `/etc` | Houses all the **system and application configuration files**. |
| `/usr` | Contains user binaries, **system commands**, utilities, and optional configuration files. |
| `/mnt` | Provides a **temporary mount point** for mounting external file systems (e.g., external drives). |

## Key System Files

| File Path | Description |
| :--- | :--- |
| `/etc/passwd` | The **user database file** containing usernames, user IDs (UIDs), and account details. |
| `/etc/shadow` | A secure **user database file** that stores encrypted user passwords. |


# Linux Systems Administration:

## 1. File Management & Inodes

An **Inode number** is a unique reference number used by the filesystem to locate a file's physical data blocks on a Hard Disk. 

*   **Identity:** Every distinct file has its own unique Inode number.
*   **Path Resolution:** A logical path (e.g., `/abc`) is simply a human-readable pointer used to fetch the physical object on the hard drive via its assigned Inode number.
*   **Checking Inodes:** Use the `ls -ilh` command to display Inode numbers. You can append a specific file name to target it directly:
    ```bash
    ls -ilh /path/to/file.txt
    ```

### Links: Symlinks vs. Hardlinks

| Feature | Symlinks (Symbolic / Soft Links) | Hardlinks |
| :--- | :--- | :--- |
| **Concept** | An alternate shortcut path pointing to an existing file path. | An alternate direct path pointing straight to the physical object. |
| **Inode Number** | **Different** from the parent file. It calls the parent path, which then fetches the data. | **Identical** to the parent file. Both paths point directly to the same Inode. |
| **Quantity** | A single file can have multiple symlinks. | A single file can have multiple hardlinks. |
| **Parent Deletion** | If the parent file is deleted, the symlink breaks and data is lost. | If the parent path is deleted, the data is still accessible via the hardlink. |
| **Creation Command** | `ln -s <target_file> <link_name>` | `ln <target_file> <link_name>` |
| **Example** | `ln -s /usr/local/abc.txt /root/xyz` *(Creates shortcut `xyz`)* | `ln /root/abc /usr/def` *(Creates direct link `def`)* |

---

## 2. Process & Service Management

### Understanding Processes
*   **Definition:** Processes are active, running applications residing in RAM. They consume hardware energy (CPU cycles and memory allocation) to execute.
*   **Process ID (PID):** Every active process is automatically assigned a unique PID.
*   **PID 1:** Reserved exclusively for the **INIT** (or `systemd`) process, which is the very first process that boots up in Linux.
*   **Types:** Divided cleanly into **System-initiated** processes and **User-initiated** processes.

### Execution Spaces
*   **Kernel Space:** Runs the `kthread` process, which manages and spawns all low-level kernel processes.
*   **User Space:** Runs the `systemd` process, which manages and spawns all user-level applications and services.

### Process Priority & Performance Tuning
Every process starts with a default priority. Administrators can manually adjust this priority to allocate more or fewer CPU cycles/RAM resources.
*   **Nice Value:** Used to configure process priority.
*   **Range:** Scale spans from **-20 to +19**.
*   **High Priority:** **-20** represents the highest possible priority (least "nice" to other processes).
*   **Low Priority:** **+19** represents the lowest possible priority.

### Services
*   **Definition:** A service is a background script or program that manages (starts, stops, or restarts) the lifecycle of an application's processes.
*   **Storage Path:** All system service files are natively stored in:
    ```path
    /usr/lib/systemd/system
    ```
*   **Emergency Mode:** If the system crashes or fails a normal boot cycle, administrators can manually drop into **Emergency Mode**. This grants a raw recovery console with root privileges for troubleshooting.

### Core Management Commands
*   **List Processes:** `ps -el` (Lists currently running processes with full details).
*   **Kill by PID:** `kill <PID>` (Terminates a specific process using its ID).
*   **Kill by Name:** `pkill <NAME>` (Terminates processes matching a specific application string).

---

## 3. Dynamic Kernel Tracing with eBPF

- It is extended Berkley packet filter
- It provides functionality for dynamic kernel tracing without requiring special kernel modules (e.g. SystemTap) or Kernel recompile and system reboot (e.g. debug kernel)
- ‘Bcc-tools’ consists of a large collection of dynamic kernel tracing tools designed to work with eBPF technologies and provide details about system performance.
- It collects a wide variety of information such as kernel data, system latency, application performance and language performance monitoring.
- ‘execsnoop’ is one of an example - This gives list of all the processes that are created using ‘exec’ command (parent process, pid, ppid)
- ‘opensnoop’ is used to monitor open system calls. When you type a command, it gives list of all the processes running in background and files touched by the kernel.
- ‘ttysnoop’ is used to monitor tty session.

### Questions

# Linux Troubleshooting Q&A Playbook

## Q. A Linux server is running but users report severe slowness. How do you troubleshoot?

### 1. Check System Load
* **Command:** `top`
* **Details Provided:** System resources, active processes, uptime, number of users, load averages, total number of processes and their states, physical RAM, virtual memory (SWAP) usage, and CPU analysis.

### 2. CPU Analysis
* **Method:** Check the percentage of CPU usage for system processes (`sy`) and user processes (`us`) inside the dynamic interface of the `top` command.

### 3. Memory Analysis
* **Commands:** `free -m` or `vmstat`
* **Purpose:** Used to quickly check system memory usage and metrics displayed in Megabytes (MB).

### 4. Disk I/O Analysis
* **Command:** `iostat`
* **Purpose:** Monitizing and collecting metrics for system input and output storage devices.

### 5. Network Analysis
* **Command:** `ss`
* **Purpose:** Socket statistics utility. Used to investigate network sockets and returns a complete list of active TCP, UDP connections, and listening ports.

---

## Q. Load average is high but CPU usage is low. What does that indicate?

* **Indication:** This state indicates that running processes are currently blocked and are not executing. 
* **Common Causes:** High Disk I/O wait times, unresolved kernel locks, or underlying physical hardware issues.
* **Diagnostic Step:** You can explicitly look for system hardware and I/O errors using the `dmesg` command.

---

## Q. What happens during Linux OOM and how do you investigate?

### System Behavior
When physical system memory is fully exhausted:
1. The Linux Kernel invokes the **OOM (Out Of Memory) Killer**.
2. The OOM Killer chooses an active process to terminate based on its `oom_score` to instantly free up memory blocks.

### Troubleshooting Workflow
* **Log Check:** Run `dmesg | grep -i oom` to scan system logs for OOM execution events.
* **Identify Process:** Find the exact process name and ID that was terminated by the kernel.
* **Review Memory:** Run `smem` to review memory usage (provides a highly accurate representation of memory footprint).
* **Investigate Leaks:** Look for underlying application memory leaks.
* **Apply Mitigation:** Apply resource restrictions using **cgroups** (a kernel feature that organizes processes into hierarchical groups to manage, restrict, and monitor resource usage).

---

## Q. A process shows high CPU but is doing little work. What do you do?

* **Identify Thread-Level Usage:** Run `top -H -p <PID>` to monitor individual threads (the smallest units of execution within a running process).
* **Identify Stack Traces:** Run `strace -p <PID>` to trace, monitor, and record real-time system calls.
* **Potential Root Cause (Deadlock/Dependency Loop):** A dependency loop where Process A is waiting on Process B, while Process B is simultaneously waiting on Process A. Both threads consume heavy CPU cycles trying to activate each other while making zero progress.

---

## Q. How do you debug a Zombie process?

* **Concept:** A Zombie process means the process completed execution but its parent process failed to call the `wait()` system call to read its exit status.
* **Identify Parent:** Run `ps -eo pid,ppid,state,cmd | grep Z` to locate the PID of the parent process.
* **Resolution:** Restart the parent process if possible. 
* **Edge Case:** If the parent process is **PID 1** (init/systemd) and remains a bug, it indicates an issue or misconfiguration within systemd itself.

---

## Q. Users can’t reach a service, but the service is running. How do you debug?
*(OR Describe your experience troubleshooting Linux system or network level issues)*

* **Local Verification:** Run `ss -lntp` to confirm the service is properly bound to the expected IP address and Port.
* **Firewall Check:** Run `iptables -L -n` to review configured network rule sets and ensure the communication path to the service is completely open.
* **Routing Check:** Run `ip route` to inspect the kernel's active routing table.
* **Connectivity Test:** Use `curl` to issue testing requests directly to the service endpoint.
* **Packet Capture:** Run `tcpdump -i eth0 port 443` to sniff incoming and outgoing network packets across the target interface.

Q. What happens when you type “ls” command ?

Shell will check if it is a builtin function, it will find its binary in /usr. If it’s not a built-in function, the shell will find the PATH variable in the directory. 
Once it finds the binary for ls, the program is loaded in memory and a system call fork() is made. This creates a child process which is ls and its parent process is shell.
Next, the ls process executes the system call execve() that will give it a brand new address space with the program that it has to run. Now, the ls can start running its program. 
Once ls process is done executing, it will call the _exit() system call with an integer 0 that denotes a normal execution and the kernel will free up its resources.
You can use strace ls to dig deeper into the system calls

Q. What is the command to check for OS information ?

cat /etc/os-release: Displays detailed OS name, version, ID, and codename

Q. Explain Boot process

1. When we power on the PC, current is sent to the Motherboard
2. Motherboard sends current to Pin 66 of the processor
3. Processor then starts generating logical signals
4. Processor then sends signal to the BIOS chip
5. BIOS chip executes BIOS program
6. BIOS program calls its interrupt 19h
7. INT 19th performs POST through which it will learn current hardware configuration
8. BIOS will save this hardware config in the form of Hardware compatibility list
9. BIOS will search for Bootable devices in HCL
10. It will first call its neighbor program “CMOS”
11. CMOS mentioned first BOOT device is Hard Drive.
12. BIOS will send its interrupt 13h to hard disk to get OS
13. BIOS understands Hard drive in the form of cylinders, heads and sectors (CHS)
14. Initially INT 13h will go to the Hard drive without any reference of CHS
15. It will then enter first sector (MBR) and bring the first file found on RAM. This file is Boot Loader. Boot loader will execute itself and will give CHS number of Kernel
16. INT 13h will then bring the kernel file on RAM with CHS number provided.
17. Kernel will then execute itself and take over the Boot Process
18. BIOS task is done and the Kernel will start loading the OS
19. Boot Loader of Linux is called GRUB
20. Kernel of Linux is called VMLINUZ
21. Kernel performs 2 tasks: hardware initialization and system initialization
22. Hardware initialization is detecting hardware, assigning suitable driver and making it ready to use. Kernel creates log of this entire process and the logs are stored in /var/log/dmesg file (‘dmesg’ command is use to see the hardware logs)
23. System initialization means to start the entire OS. First Kernel starts “systemd” program. It is the first process to start with PID 1. It initializes the system. It performs following steps:
    a. It learns default target by loading /etc/systemd/system/default.target file
    b. Every target has a ‘wants’ directory which has list of all the service files what are to be started in that target. All service files are stored in /usr/lib/systemd/system directory.
    c. To start these list of services, it runs 17 functions of /etc/rc.d/init.d/functions file in a loop
    d. Once all the services are started, it also loads ‘/etc/rc.d/rc.local’ file also known as start-up script.
24. Now, drivers of all terminals is loaded and ‘a-getty’ program is run on all the terminals. ‘a-getty’ provides the login screen and awaits username.
25. On giving username on terminal, systemd kills ‘a-getty’ and runs login program. This login program will ask for password and do AAA process to provide access.