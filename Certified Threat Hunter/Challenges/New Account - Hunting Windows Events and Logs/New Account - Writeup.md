<center><b><h1>New Account - Writeup </h1></b></center>

***



![img](https://s2.loli.net/2023/11/28/Tay2cYlNtepdHUh.jpg)

 

\- Since we’re told that the attacker created a new account, and we’re asked to get that account name. We start searching in the security event log file for a “create new account events” which has an **ID** of: **4720**

 

![img](https://s2.loli.net/2023/11/28/SNE45gwMAD2zIFV.png)

And the result is only one log which has the information we need:

![img](https://s2.loli.net/2023/11/28/UstIixX2kPeu4BH.png)

So, the created account name is: Sam. 

We get the MD5 Hash value of that name using any Hash generator like [md5hashgenerator](https://www.md5hashgenerator.com/), and the result is:

![img](https://s2.loli.net/2023/11/28/DVNLBvF1K4tPgJx.jpg)



**And our flag is**: <mark>falg{ba0e0cde1bf72c28d435c89a66afc61a}</mark>

***

Happy Practicing & Learning!

 ![Microsoft Office Signature Line...](https://s2.loli.net/2023/11/28/dIpkTqZsXwW4aiV.png)
