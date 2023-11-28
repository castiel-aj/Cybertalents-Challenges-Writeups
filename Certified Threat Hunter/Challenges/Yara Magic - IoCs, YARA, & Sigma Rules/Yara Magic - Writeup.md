<center><b><h1>Yara Magic - Writeup</h1></b></center>

***



![img](https://s2.loli.net/2023/11/28/Y5WHrtxcluADvJk.jpg)

\-    After downloading the archive file, we found a Yara rule file (rule.yara)

![img](https://s2.loli.net/2023/11/28/7W5vnRY2GEjxAVQ.jpg)

 and a folder containing binary files.

\-    Solving this challenge is easy as the rule is already existing. We have 2 choices:

1) Run Yara on windows.
2) Run Yara on Linux.

 

I choose to run it on Linux since it is already installed on my kali machine. 

\-    The syntax to run Yara is:

\#Yara option yara_rule target

And the used command is:         $yara -f rule.yara Folder 

The command will activate Yara tool with the -f option which means fast matching mode, using the rule.yara rule on the targeted folder “Folder”

And the result was:



![img](https://s2.loli.net/2023/11/28/EDz9NP8XTLtar7f.jpg)



Which means the matched file name is: 12776.

And the flag is: <mark>flag{12776}</mark>

***

Happy Practicing & Learning!

 ![Microsoft Office Signature Line...](https://s2.loli.net/2023/11/28/UB1LI5EmKGXh9tC.png)
