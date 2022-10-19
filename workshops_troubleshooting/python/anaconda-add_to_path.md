# Add anaconda to the path

This is an optional step. This is for the case where you didn't check the box in step 6 duing installation and now want to add Anaconda to your Path. The advantage of this is that you will be able to use Anaconda in your Command Prompt, Git Bash, cmder etc.

## Problem

If you type in git bash 

```bash
conda --version
python --version
```
If you get the right panel you are safe, if you get the left, then you need to add Anaconda to your environment variables. 

![](./images/anaconda_found_notfound_bunq4v.png)


## Solution

If you don't know where your conda and/or python is, open an Anaconda Prompt and type in the following commands. This is telling you where conda and python are located on your computer.

```bash
where conda
where python
```

![](./images/anacondaPrompt_RED_gvxfea.png)

- Add conda and python to your PATH. You can do this by going to your Environment Variables and adding the output of step 3 (enclosed in the red rectangle) to your path. If you are having issues, here is a short [video](https://youtu.be/mf5u2chPBjY?t=15m45s) on adding conda and python to your PATH.

![](./images/environmentVariablesAddedToPATH_aee7yf.png)


-  Open a new Command Prompt. Try typing `conda --version` and `python --version` into the Command Prompt to check to see if everything went well.

![](./images/condaFoundDone_1_g3qnuj.png)