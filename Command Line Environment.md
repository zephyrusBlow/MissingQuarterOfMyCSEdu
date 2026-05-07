---
title: Command Line Environment

---

# Command Line Environment
## Arguments
- Shell programs receive a list of arguments when they are executed. Arguments are plain strings in shell, and it is up to the program how to interpret them. 
e.g. when we do ls -l folder/, we are executing the program /bin/ls with arguments ['-l', 'folder/'].
- see the last part of the shell note
## Streams of arguments
- command run in pipeline: they run in parallel (starting in the order of input) unless you command them to start once another one is over
- every program has two output streams: `stdout` and `stderr`
    - `stdout`: the one most commonly encountered and it is the one that is used for piping the output of the program to the next command in the pipeline
    - `stderr`: an alternative stream that is intended for programs to report warnings and other types of issues, without that output getting parsed by the next command in the chain.
## Environment variables
- To assign variables in bash we use the syntax `foo=bar`, and then access the value of the variable with the `$foo` syntax
- Shell variables do not have types, they are all strings
## Return codes
- By default a shell script will return exit code 0
meaning "everything went well!"
- To return a nonzero exit code we have to use the `exit NUM` shell built-in, access the return code of the last command that was run by accessing the special variable `$?`
- `&&` for AND, `||` for OR operations
- `if` and `while` statements use return codes to make decisions
## Signals
- e.g. interrupt a process with `Ctrl+C`
what happens is 
    1. keyboard pressing Ctrl+C
    2. shell identifies the special combination
    3. the shell process sends a SIGNIT signal to the running process
    4. the signal interruppts the execution of the runnning process
- samples
`$ sleep 1000
^Z
[1]  + 18653 suspended  sleep 1000`
`$ nohup sleep 2000 &
[2] 18745
appending output to nohup.out`
`$ jobs
[1]  + suspended  sleep 1000
[2]  - running    nohup sleep 2000`
`$ kill -SIGHUP %1
[1]  + 18653 hangup     sleep 1000`
`$ kill -SIGHUP %2   # nohup protects from SIGHUP`
`$ jobs
[2]  + running    nohup sleep 2000`
`$ kill %2
[2]  + 18745 terminated  nohup sleep 2000`
## Remote machines
- SSH (secure shell)
connect to a remote server and provide the shell interface
    - connect with a command like `ssh Sinecurist@server.northwestern.edu`
    - able to run commands non-interactively: send command from local host to server without entering remote server, improve proficiency
    connect $\rightarrow$ operate command $\rightarrow$ return output to local host $\rightarrow$ automatically disconnect
    - via passswords or ssh keys for authentication; to generate keys, run `ssh-keygen`
    - able to transfer files from and to the server securely, like using `scp` tool `scp path/to/localFileName remote_host:path/to/remoteFileName`
    
## Terminal multiplexers
- e.g. `tmux` helps you to multiplex terminal windows to interact with multiple shell sessions side by side
- common commands for `tmux`
    - Sessions: a session is an independent workspace with one or more windows
`tmux` starts a new session.
`tmux new -s NAME` starts it with that name.
`tmux ls` lists the current sessions
Within `tmux` typing `<C-b> d` detaches the current session
tmux a attaches the last session. You can use `-t` flag to specify which
    - Windows: equivalent to tabs in editors or browsers, they are visually separate parts of the same session
`<C-b> c` Creates a new window. To close it you can just terminate the shells doing `<C-d>
`<C-b> N` Go to the N th window. Note they are numbered
`<C-b> p` Goes to the previous window
`<C-b> n` Goes to the next window
`<C-b> ,` Rename the current window
`<C-b> w` List current windows
    - Panes: like vim splits, panes let you have multiple shells in the same visual display.
`<C-b> "` Split the current pane horizontally
`<C-b> %` Split the current pane vertically
`<C-b> <direction>` Move to the pane in the specified direction. Direction here means arrow keys.
`<C-b> z` Toggle zoom for the current pane
`<C-b> [` Start scrollback. You can then press `<space>` to start a selection and `<enter>` to copy that selection.
`<C-b> <space>` Cycle through pane arrangements.

## Customizing the Shell
- 看你的开发环境咯，什么简写abbreviation缩写aliases全部吻了上来

## AI in the shell
- tools like `simonw/llm` can help you generate shell commands
- LLMs can be integrated into shell pipelines
    e.g. ```$ cat users.txt
Contact: john.doe@example.com
User 'alice_smith' logged in at 3pm
Posted by: @bob_jones on Twitter
Author: Jane Doe (jdoe)
Message from mike_wilson yesterday
Submitted by user: sarah.connor
$ INSTRUCTIONS="Extract just the username from each line, one per line, nothing else"
$ llm "$INSTRUCTIONS" < users.txt
john.doe
alice_smith
bob_jones
jdoe
mike_wilson
sarah.connor```
- tools like Claude code act as a meta-shell