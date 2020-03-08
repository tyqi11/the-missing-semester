# The Missing Semester Note

My operating system: Ubuntu 16.04

## The Shell

https://missing.csail.mit.edu/2020/course-shell/

### Navigating in the shell

- `ls - l`

  `drwxr-xr-x 1 root root [size] [date] ..`

  `d` for a directory, `-` for a file

  three characters in a group, `r` for read, `w` for write, and `x` for execute, `-` for not have

- `mv` for move, two
- `cp` for copy
- `rm` for remove, `rmdir` for removing an empty directory
- `mkdir` for making a directory

### Connecting programs

* redirection
  * `echo hello > hello.txt `
  * `cat < hello.txt > hello2.txt`
* pipes
  * `ls -l / | tail -n1`

### A versatile and powerful tool

`sudo`: *do* something as *su* ("super user" or root)