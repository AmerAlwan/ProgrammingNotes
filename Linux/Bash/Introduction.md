# Introduction

A shell interprets user commands, either provided by the user directly or read from a file called the shell script or shell program.

Shell scripts are interpreted, not compiled, meaning commands are read line per line. Unlike a compiler, which converts a program into machine readable form, an executable file, which may then be used in a shell script.

## Shell Types

### Bourne Shell

A Bourne Shell (`sh`) is the original shell stull use don UNIX systems. It is a basic shell with few features. It is not the standard shell

### Bourne Again Shell (Bash)

The Bourne Again Shell (Bash) is the most standard shell for its intuitiveness and flexibility. Bash is the superset of the Bourne shell as it is like containing a set of plugins and addons. That means that Bourne shell commands are compatible with Bash, but that is not always the case in the reverse

### C shell (`csh`)

A shell with syntax resembling the C programming language

### TENEX C Shell (`tcsh`)

A superset of the common C shell, enhancing user-friendliness and speed

## Executing Commands

Normal programs are system commands that exist in compiled form on a system. 

**Forking: **A procedure that occurs when a program is run and Bash makes an exact copy of itself with a different process ID number and which runs on a different process

**Exec:** After the forking process, the address space of the child process is overwritten with the new process data through an `exec` call to the system