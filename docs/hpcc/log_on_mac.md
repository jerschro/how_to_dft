[:fontawesome-solid-house:](../index.md) :fontawesome-solid-angle-right: [HPCC](index.md) :fontawesome-solid-angle-right: **Logging onto HPCC Mac**

# Log on For Mac Devices

## Instructions to Log On for the First Time

1. Make sure you are on the wifi network TTUNet. If you are off campus, look at the [VPN Instructions](connect_to_vpn.md) to be able to log in.
1. Open terminal for mac. (++cmd+t++ is a shortcut to open the Terminal)
1. Type command "ssh eraider@login.hpcc.ttu.edu" where eraider is your eraider account name.
1. You are now on the super computer!
1. Go to [Intro to the Terminal](intro_to_terminal.md) to learn how to interact with it!

## Recommended Software to download locally on Mac

In order to do our research correctly we need different categories of programs.
We need a visualization software to be able to see the molecular models.
We need a good text editor to be able to see the output files of the DFT programs.
For Mac, you need to download XMING to get x forwarding.
It is also a good idea to have a coding environment downloaded locally to be able to program.

* [VESTA](https://jp-minerals.org/vesta/en/download.html) (Visualization Software) :fontawesome-solid-star:
* [JMOL](https://jmol.sourceforge.net/download/) (Visualization Software) :fontawesome-solid-star:
* [TTMolE](https://jerschro.github.io/ttmole_documentation/) (Created In House Visualization Software) :fontawesome-solid-star::fontawesome-solid-star::fontawesome-solid-star:
* [Avogadro](https://avogadro.cc/) (Visualization Software)
* [Avogadro2](https://two.avogadro.cc/install/index.html) (Visualization Software)
* [XQuartz](https://www.xquartz.org/) (X-11 Forwarding Software) :fontawesome-solid-star:
* [sublime](https://www.sublimetext.com/) (Text Editor)
* [VSCode](https://code.visualstudio.com/) (Text Editor) :fontawesome-solid-star:
* [Anaconda/Conda](https://conda.io/projects/conda/en/latest/user-guide/install/index.html) (Coding Environment)
* [iTerm2](https://iterm2.com/downloads.html) (Mac Terminal Replacement for easy Customization)

:fontawesome-solid-star: Programs with a Star are HIGHLY recommended to use.

## How to Open Molden (aka Turn on X-11 Forwarding) on Mac

1. Download [XQuartz](https://www.xquartz.org/)
2. Add "export PATH=/home/rnieman/PROGRAMS/molden6.2/:$PATH" to .bashrc file
3. When you type ssh command to open terminal add the -X -Y flag so "ssh -X -Y eraider@login.hpcc.ttu.edu"
4. Use command "molden [filename]" to open molden 

## How To Transfer Files Locally

1. Use scp function in local terminal.
1. Use Global Transfer web server.