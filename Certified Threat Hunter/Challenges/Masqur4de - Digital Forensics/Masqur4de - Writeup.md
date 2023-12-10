<center><b><h1>Masqur4de</h1></b></center>

***

![image-20231210171012933](https://s2.loli.net/2023/12/10/EcgLbQy19BT4iJl.png)



\- The challenge provides us a **memory dump** file, so we need to solve this challenge using the **Voltality3** tool. 

We start with **pstree** plugin of volatility to check processes and parent process of each one:

#**python vol.py -f Masqur4de.mem windows.pstree**

![image-20231210172039982](https://s2.loli.net/2023/12/10/uOkQbAGPq3tRCaB.png)

\- There is a prcoess hidning "masqurading" behind normal windows process "svchost.exe". This process must have a parent process "services.exe", but in the image it started from "explorer.exe"!!!

So, we need to get this process file to check it using this command: 

#**python vol.py -f Masqur4de.mem -o FilesOut windows.dumpfles --pid 3588**

![image-20231210172437597](https://s2.loli.net/2023/12/10/K2tyibJkGw3WqXE.png)

\- Now that we know that it started from an **image** file, we check this image file on **Virustotal**. And indeed the file is malicious.

We go to **relations** tab to see the domain names that the malicious file is communication with:

![image-20231210172742053](https://s2.loli.net/2023/12/10/dwr5uJfSWDkRqCT.png)

and our flag is: **FLAG{svchost_explorer_brb.3dtuts.by}**

***



Happy Practicing & Learning!

 ![Microsoft Office Signature Line...](https://s2.loli.net/2023/11/28/t28QypJLXn9lezg.png)