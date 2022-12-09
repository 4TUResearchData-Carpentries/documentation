# Objective

Having an assisting terminal window that shows the commands typed in a main terminal window. 
Additionally, the history of commands is directed to a local file, in turn pushed to a remote 
repository, which the learners can consult as logbook of the type-along activities.

# Ingredients

1) The main active terminal where the trainer does his/her typing-along. 

2) A secondary passive terminal where the history is shown. 

3) A local repository connected to a public remote repository (assumed to be web-based, assumed 
to be GitHub)

# Recipe

In the main active terminal, prescribe that the history file `~/.bash_history` is refreshed 
each time a new line is created:

`export PROMPT_COMMAND="history -a; $PROMPT_COMMAND"`

In the passive terminal use the capabilities of `tail` to visualize the growth of a file's tail 
with the option `-f`. The standard output to screen is duplicated and directed to a file in the 
local repository with `tee`:

`tail -n 0 -f ~/.bash_history | tee $FILE`

The option `-n 0` in conjunction with `-f` means that the first block on record will be the 
next command, instead of the default past ten command. Unequivocal for the leaners.

# Special issues with Git

`gitautopush` pushes the entire repository when a change is detected in a selected folder. This 
is not a problem for the workshop on Unix Shell, insofar as the instructor does not uses Git 
repository AND does not need to keep control on the status-add-commit cyle. On the contrary, 
this loss of control is annoying and counterproductive for the Git workshop.

A viable solution depends on which repo one places the target file of tee.

For Git workshop, placing the redirected tail anywhere inside the same repository used by the 
instructor is disruptive: gitautoupdate will push every change automatically. Also fragile is 
creating an ad-hoc branch 'notes', starting the gitautopush task from that branch, and 
pushing into a namesake branch; switching branches modifies the target file in the 
local directory, which breaks the redirection of the `tail -f` command. The fact that 
the target file keeps its name across a branch switch does not help restore the broken redirection.

A friendly option is to redirect the tail to a separate passive repository. In that case, the 
instructor ends up preparing more repos for the same workshop. The solution of Maurits Kok for 
Python has been to create a software_carpentry repo for delivering its content, and a 
software_carpentry_learners automatically updated as the workshop runs. A local repo cloned 
from the latter should host the redirected command history. Note that the Python workshop does 
not use Git. There is no need to isolate the log file in a separate branch, such as 'notes'.

# Credits

Maurits' websites...
