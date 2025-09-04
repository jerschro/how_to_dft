[:fontawesome-solid-house:](../index.md) :fontawesome-solid-angle-right: [HPCC](index.md) :fontawesome-solid-angle-right: **Connect to TTU VPN**

# Steps to Connect to TTU VPN

When you are not on campus connected to the wifi TTUnet, you will need to use the TTU VPN to gain access to the HPCC.


1. Follow the steps on this IT website or written out below: [https://askit.ttu.edu/vpn](https://askit.ttu.edu/vpn). The following steps below are also found on the IT VPN article.
2. You need to request access for it, by calling IT help central to have them approve it or using this link: [https://askit.ttu.edu/sp?id=sc_cat_item&sys_id=a990ee5ddbdf41144d17266e139619f8](https://askit.ttu.edu/sp?id=sc_cat_item&sys_id=a990ee5ddbdf41144d17266e139619f8). The reason can be "To access TTU HPCC off campus."
3. Download the Global Protect VPN App:
    * Windows Instructions: [https://askit.ttu.edu/kb_view.do?sysparm_article=KB0025277](https://askit.ttu.edu/kb_view.do?sysparm_article=KB0025277)
    * Mac Instructions: [https://askit.ttu.edu/kb_view.do?sysparm_article=KB0025278](https://askit.ttu.edu/kb_view.do?sysparm_article=KB0025278)
4. Once the VPN App is downloaded, you can connect to it by following the instructions below:
    * Windows Instructions: [https://askit.ttu.edu/kb_view.do?sysparm_article=KB0024975](https://askit.ttu.edu/kb_view.do?sysparm_article=KB0024975)
    * Mac Instructions: [https://askit.ttu.edu/kb_view.do?sysparm_article=KB0024977](https://askit.ttu.edu/kb_view.do?sysparm_article=KB0024977)
5. To disconnect, follow the instructions below:
    * Windows Instructions: [https://askit.ttu.edu/kb_view.do?sysparm_article=KB0025238](https://askit.ttu.edu/kb_view.do?sysparm_article=KB0025238)
    * Mac Instructions: [https://askit.ttu.edu/kb_view.do?sysparm_article=KB0025240](https://askit.ttu.edu/kb_view.do?sysparm_article=KB0025240)


## Linux

TTU IT does not officially support the Global Protect VPN for Linux even though they have a user guide on it. These instructions are accurate as of 9/3/25 for Jeremy.

1. If you have Linux or have Mac and want a cli vpn app, download this github cli tool: [https://github.com/yuezk/GlobalProtect-openconnect](https://github.com/yuezk/GlobalProtect-openconnect). 
2. Once you type the vpn address, ```vpn.ttu.edu```, then it should work as normal in a running terminal window.
3. You can make an alias like below for ease of use:
    * ```alias vpn="sudo -E gpclient connect --browser default vpn.ttu.edu"```

<!-- 

2. There is also a multifactor authentication you will have to set up. Follow this link for the instructions: [https://www.askit.ttu.edu/mfa](https://www.askit.ttu.edu/mfa)
3. I believe you need to request access for it, by calling IT help central to have them approve it or using this link: [https://askit.ttu.edu/sp?id=3Dsc_cat_item&sys_id=3Da990ee5ddbdf41144d17266e139619f8](https://askit.ttu.edu/sp?id=3Dsc_cat_item&sys_id=3Da990ee5ddbdf41144d17266e139619f8) 

-->


