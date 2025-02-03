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

## To Install Conda Locally

Follow Conda instructions for your operating system.

* [Linux](https://conda.io/projects/conda/en/latest/user-guide/install/linux.html)
* [Mac](https://conda.io/projects/conda/en/latest/user-guide/install/macos.html)
* [Windows](https://conda.io/projects/conda/en/latest/user-guide/install/windows.html)

