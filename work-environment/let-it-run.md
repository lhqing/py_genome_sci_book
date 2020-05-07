---
description: How to keep your command running?
---

# Keep Running

Here I introduce two ways to keep your command running in the background. You need this when:

* Run a command \(e.g., downloading a large file\) that takes a long time to finish.
* Run a command in the background for a long time, for example, a [jupyter notebook server](jupyter-notebook.md).

## SIGHUP

When you execute a command in the terminal, it will block other commands until it finishes. If you close the terminal during the execution, the command will terminate also. Because a [SIGHUP](https://en.wikipedia.org/wiki/SIGHUP) will be sent to that process \(the executing program\), and terminate it. Below prevent this from happening even you close the terminal.

## Run with nohup and &

`nohup` is a simple way to keep your command running, it means "no SIGHUP", so if you use `nohup` in front of a command, closing terminal will not terminate the command.

"&" means put the process will be put in the background, so it will not block terminal, and you can execute other commands in this same terminal.

Check out `fg`, `bg` , and `jobs` command again [here](http://linuxcommand.org/lc3_lts0100.php).

```bash
# Use the sleep command to mimic a long execution time.
$ sleep 100
# This will block terminal for 100s. 
# Close terminal also terminates this.

$ nohup sleep 100
# This will still block terminal for 100s. 
# But close terminal will not terminate this.

$ nohup sleep 100 &
# This will not block terminal. 
# Close terminal will not terminate this.

$ jobs
[1]  + running    nohup sleep 100
# Use jobs command, you can see this job right now run in the background

$ fg
[1]  + 5741 running    nohup sleep 100
# Use fg, we move the command back to the foreground
# It blocks the terminal again
# If I press Ctrl+Z in here:
^Z
[2]  + 5741 suspended  nohup sleep 100

# it says this job is suspended
# use bg now can put it back to the background and start running
$ bg
[2]  - 5741 continued  nohup sleep 100
```

## Screen

`screen` is an even better way. It can create named terminal screens, which will keep running independently to your terminal. Here are a few examples

```bash
# Create a screen called jupyter
$ screen -R jupyter

# when executed above command, the terminal seems refreshed, 
# this is because you entered a new screen

# now I start a jupyter notebook server (explained in another page)
$ jupyter notebook --ip=localhost --port=8888
(skip output)
# this will keep running to provide me the jupyter notebook service

# now let's exit screen
# press ctrl+A first, then press d
# ctrl+A enters screen control, d means detach
^Z
d

# now terminal change back, and I saw this:
$ screen -R jupyter
[detached]

# Jupyter is still running!

# we can check all running screens
# we can open many screens
$ screen -ls
There is a screen on:
	5892.jupyter	(Detached)

# we can go back to screen by name or id at any time
$ screen -r jupyter

# now terminal change to the jupyter one
```

I will leave other usages of `screen` as homework, you can quickly learn this from google and youtube since you now know what to search 😏.

* How to terminate a screen?
* What's other options to control a screen when you press Ctrl+A in a screen?



