[:fontawesome-solid-house:](../index.md) :fontawesome-solid-angle-right: [HPCC](index.md) :fontawesome-solid-angle-right: **How to Install Conda**


# How To Install Conda

## To Install Conda Locally

If you want MiniForge locally, find your operating system [Here](https://conda-forge.org/download/).

Follow Conda instructions for your operating system.

* [Linux](https://conda.io/projects/conda/en/latest/user-guide/install/linux.html)
* [Mac](https://conda.io/projects/conda/en/latest/user-guide/install/macos.html)
* [Windows](https://conda.io/projects/conda/en/latest/user-guide/install/windows.html)

## To Install Conda on HPCC

Follow the HPCC tutorial on how to install Miniforge/Conda, check out the link [here](https://www.depts.ttu.edu/hpcc/userguides/application_guides/Miniforge.php). The installation instructions are in the **Installing MiniForge** section.

<!-- Following the below code will automatically install conda on the HPCC. Old Link [here](https://www.depts.ttu.edu/hpcc/userguides/application_guides/python.local_installation.php). 
``` bash
#  Running the following script will automate the process of installing a local copy of Miniconda v3
/lustre/work/examples/InstallPython.sh

#  Once complete you will need to run the following commands before you can actually use the new environment you created.
. $HOME/conda/etc/profile.d/conda.sh
conda activate
 
```
-->

**If the Miniforge installation does not automatically add something to your .bashrc, please follow the instructions below. 8/25/25**

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

## Notes on Conda Commands

1. Version:
    * ```conda --version```

1. Update:
    * ```conda update conda```

1. Create environment:
    * ```conda create --name [name] [pkg(s)]```
    * ex: conda create --name test_environment pandas

1. List all environments (The asterisk * in it's output will indicate the active environment)
    * ```conda info --envs```

1. Python Version:
    * ```python --version```

1. List current packages in the active environment:
    * ```conda list```

1. List all environments you have:
    * ```conda list -env```

1. Search anaconda repository for a desired package:
    * ```conda search [pkg]```

1. Install a specific package to the active environment:
    * ```conda install [pkg]```

* Good Packages To Install for Python:
    * numpy
    * matplotlib
    * scipy
    * pandas
    * tabulate
    * 
* Other python modules that are standard and already installed in Python:
    * os
    * sys
    * shutil
    * textwrap
    * argparse

## Other Documentation for Conda

[TTU HPCC](https://www.depts.ttu.edu/hpcc/userguides/application_guides/Miniforge.php) has good documentation on Conda. [Conda website](https://docs.conda.io/en/latest/) has good documentation also.
