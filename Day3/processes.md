# Processes

In memory, possibly uses the CPU.

System process provide services such as logging rather than a user interface.

`ps` - lists all user processes

`ps -e` - lists all processes including system processes

TTY in the process lists shows the terminal session related to the process

`kill {pid}` - kills a process

`kill -9 {pid}` - brute force kill a process if the command above does not work.

Do not brute force kill a parent process as this will create zombie processes, they use memory and take up resources.