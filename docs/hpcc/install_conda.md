[:fontawesome-solid-house:](../index.md) :fontawesome-solid-angle-right: [HPCC](index.md) :fontawesome-solid-angle-right: **How to Install Conda**


# How To Install Conda

## To Install Conda on HPCC

Following the below code will automatically install conda on the HPCC. For more information, check out the link [here](https://www.depts.ttu.edu/hpcc/userguides/application_guides/python.local_installation.php).

``` bash
#  Running the following script will automate the process of installing a local copy of Miniconda v3
/lustre/work/examples/InstallPython.sh

#  Once complete you will need to run the following commands before you can actually use the new environment you created.
. $HOME/conda/etc/profile.d/conda.sh
conda activate
 
```

Once you install conda on the HPC. You need to add the 1 of the 2 choices below to your .bashrc file in order activate conda automatically when you login to the HPC. Choice 1 is the simplier option compared to choice 2 which includes some error checking but causes issues when others try to source your conda environment. You will need to replace $USER with your eraider.

Choice 1 - Simplier Conda Activation

``` bash
source /home/$USER/conda/etc/profile.d/conda.sh
export PATH=/home/$USER/conda/bin:$PATH
conda activate

```

Choice 2 - Error Checking Conda Activation

``` bash
# >>> conda initialize >>>
# !! Contents within this block are managed by 'conda init' !!
__conda_setup="$('/home/$USER/conda/bin/conda' 'shell.bash' 'hook' 2> /dev/null)"
if [ $? -eq 0 ]; then
    eval "$__conda_setup"
else
    if [ -f "/home/$USER/conda/etc/profile.d/conda.sh" ]; then
        . "/home/$USER/conda/etc/profile.d/conda.sh"
    else
        export PATH="/home/$USER/conda/bin:$PATH"
    fi
fi
unset __conda_setup
# <<< conda initialize <<<

```

## To Install Conda Locally

Follow Conda instructions for your operating system.

* [Linux](https://conda.io/projects/conda/en/latest/user-guide/install/linux.html)
* [Mac](https://conda.io/projects/conda/en/latest/user-guide/install/macos.html)
* [Windows](https://conda.io/projects/conda/en/latest/user-guide/install/windows.html)

