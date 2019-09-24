

# Overview
The aim of this document is to provide information about how to set up a "command history" for the bash environment.

### Motivation
During the Software Carpentry workshops (especially the Bash and Git tutorials), we had noticed there are several cases in which participants ask the instructor to show the last issued command. This is usually because as soon as a command is run, the output quickly clogs up the screen and hides the actual command. Although we are making use of the Etherpad to mitigate this effect, sometimes even the person in charge of typing them on the Etherpad might have trouble finding the latest command and has to ask the instructor to scroll up. Additionally, the action of tabbing back and forth between the terminal and Etherpad might prove distracting for the participants and make them miss out on the information as they are trying to search for the command which was just issued.

### Command History to the rescue
To provide a solution, we propose the **command history** window. Once setup, this window is able to show the last issued commands on the terminal in real time. The benefit is that the instructor no longer needs to worry about scrolling up and down to find and show the commands. Although there are multiple ways to achieve this functionality, our goal is to make the changes minimalistic and portable to both Windows and Unix environments.

### Tested on

- Windows 10 with Git Bash (success!)

# Setup
We are going to have two terminal windows:
1. **Main terminal**: used by the instructor to issue commands and shows the output.
2. **Command history terminal**: The other terminal which automatically updates itself to show the latest issued commands in the main terminal.

For convenience reasons, we are going to refer to these windows as #1 and #2 respectively.  

### Step 0 (Only for macOS with El Capitan+ version):
On any terminal, issue the following command:<br>
`touch ~/.bash_sessions_disable`<br>

This is needed for El Capitan+ macOS version to disable to per-session command history. This sets the $HISTFILE variable back to .bash_history instead of a unique temporary file. Make sure you open new terminals for the next steps, so that this change would be applied for them.


### Step 1:
On the main terminal (#1), issue the following command:

`export PROMPT_COMMAND="history -a;$PROMPT_COMMAND"`

By default, the command history file is only updated once the terminal exits. This line forces the bash to update the .bash_history file, after every command so that its effect would be immediately available.
### Step 2:
On the command history terminal (#2), issue the following command:

`tail -f ~/.bash_history`

This shows the content of .bash_history file and updates itself whenever something is appended to the file.

### Result
At this point, terminal #2 should be showing any issued commands from terminal #1. The instructor may resize terminal #2 to only show last X number of commands instead of the whole history.


### Do I have to do anything to revert these changes?
Since we are using `export` to modify the `PROMPT_COMMAND` variable, the effect is only seen in the current terminal. This means that just closing the terminal #1 is enough to revert the change. This also means that if the instructor accidentally closes terminal #1, then they would have to redo Step 1.

If you had to do Step 0 (macOS El Capitan+), and want to go back to per-session command history, simply run:<br>
`rm ~/.bash_sessions_disable`


# Troubleshooting
This section will be used in the future to add corner cases.
