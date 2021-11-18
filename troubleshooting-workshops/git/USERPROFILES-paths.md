The student works with "Linux+Win10". The problems appear to relate with environment variable for the home directory or namely %USERPROFILES. They have several manifestations:

### 1) Configuration for 

`git config --global user.name "A.N. Other"  # also for user.email`

returns  

`error: GitBash "could not lock config file %USERPROFILES/.gitconfig"`

Workaround: invert the order of the lecture; *first* create a .git repository and *then* set user.name and user.email as local variables (only for the current repository), like this:

`git config --local user.name "A.N. Other"`

Result: pass.

### 2) Creation of the ssh keypair

When using `ssh-keygen` to create a keypair, the system has %USERPROFILES/.ssh as defaultm which cannot be found

Workaround: create a ssh key pair locally in the Carpentries working directory, like

`mkdir [working directory]/.ssh` 

and pick up the public key for GitHub from here. 
It is necessary to pick up the private key from there too:

`ssh -i [working directory]/.ssh -T git@github.com`

Result: unreported
 
### 3) Go to home directory

`cd ~` expands to the absolute path of the Desktop, so if you launch that command from any other directory it complains about a directory not found

Workaround: do not use the tilde and give the path explicitly in a `cd` command.

Result: pass.

### Status

The student lagged behind, had to stop practising  and could only follow by listening.

Issue not really solved at the root. Arguably, a misconfigured environment variable is the root cause. The problem could have been caused by a wrong configuration setting of Git Bash (a suggestion of Susanne's, not tested).
