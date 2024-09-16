[:fontawesome-solid-house:](../index.md) :fontawesome-solid-angle-right: [HPCC](index.md) :fontawesome-solid-angle-right: **The .bashrc File**
# The .bashrc file

The .bashrc file is a file in your home directory that sets up your kernel environment every time you log onto the HPCC.
In order to be more efficient, we make custom commands aka aliases to make our lives easier.
We also need to add specific modules and settings to our local bash environment in order for the DFT programs to run.
The .bashrc file is located in your home directory.

## Steps to Edit and "Refresh" your .bashrc file

1. Use your text editor of choice. The file path is always `~/.bashrc`
2. Add or change the lines of the .bashrc file.
3. Save the changes.
4. Run the command `source ~/.bashrc` 
    * This command will rerun your .bashrc file and apply the changes you made to the linux environment.
    * It is also suitable to log out and log back into the terminal to "refresh" your .bashrc file.

## Commands Needed for Turbomole

If you are using Turbomole, you will need to have these lines in your .bashrc file in order for Turbomole to run correctly.

``` bash
export TURBODIR=/home/hlischka/programs/TURBOMOLE-7.5/TURBOMOLE
source $TURBODIR/Config_turbo_env
export PATH=$TURBODIR/scripts:$PATH
export PATH=$TURBODIR/bin/`sysname`:$PATH

``` 

## Aliases Recommended for Ease of Use

Replace eraider with your eraider/hpcc account name.

``` bash
alias sq=' squeue -u eraider '
alias lus=' cd /lustre/scratch/eraider '
alias work=' cd /lustre/work/eraider '
alias li=' ls -r -lah --color=auto '
alias vi='vim'
alias size='du --summarize --human-readable * '

```

## To automatically activate conda

``` bash
# >>> conda initialize >>>
# !! Contents within this block are managed by 'conda init' !!
__conda_setup="$('/home/jerschro/conda/bin/conda' 'shell.bash' 'hook' 2> /dev/null)"
if [ $? -eq 0 ]; then
    eval "$__conda_setup"
else
    if [ -f "/home/jerschro/conda/etc/profile.d/conda.sh" ]; then
        . "/home/jerschro/conda/etc/profile.d/conda.sh"
    else
        export PATH="/home/jerschro/conda/bin:$PATH"
    fi
fi
unset __conda_setup
# <<< conda initialize <<<

```

## For molden

``` bash
alias molden='/lustre/work/rnieman/molden6.9/bin/molden'

```

## For Sublime

``` bash
alias subl='/home/tristfis/PROGRAMS/sublime_text_3/sublime_text $1'

```

## For Jeremy's Squeue Scripts

``` bash
alias check_sq='bash /home/jerschro/Scripts/squeue/read_squeue.sh'
alias check_abuse='bash /home/jerschro/Scripts/squeue/pandas_squeue.sh'
alias nocona_pie='bash /home/jerschro/Scripts/squeue/nocona_pie.sh'
alias quanah_pie='bash /home/jerschro/Scripts/squeue/quanah_pie.sh'

```

## For TTMole

``` bash
alias ttmole='/home/jerschro/conda/bin/python3 /home/jerschro/Programs/TTMolE/main.py'

```

