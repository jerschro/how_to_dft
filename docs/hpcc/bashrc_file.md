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
export TURBODIR=/home/aaquino/Programs/TURBOMOLE

source $TURBODIR/Config_turbo_env

export PATH=$TURBODIR/scripts:$PATH
export PATH=$TURBODIR/bin/`sysname`:$PATH
``` 

## Aliases Recommended for Ease of Use

Replace eraider with your eraider/hpcc account name.

``` bash
alias sq=' squeue --me '
alias lus=' cd /lustre/scratch/eraider '

```