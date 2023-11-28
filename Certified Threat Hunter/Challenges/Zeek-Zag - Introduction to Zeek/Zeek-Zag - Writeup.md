<center><b><h1>Zeek-Zag - Writeup</h1></b></center>

***



![img](https://s2.loli.net/2023/11/28/vjmIfPNuL8swrBq.jpg)



To solve this challenge, we need to analyze the captured traffic file. We can do this by uploading the file into an online packet analyzer like [apackets](https://apackets.com/upload). However, the challenge is about getting used to using **Zeek** tool. So, we’ll use Zeek tool to solve it.

\-    First, we click on the <b>shell.php</b>, and it opens up a shell for use.

​              ![img](https://s2.loli.net/2023/11/28/5EHTA8uSIP4Xxpy.png)

 

 Here, we list the files in our current directory and find that there is only 2 files (the .pcap file, and the shell.php). So, we try to analyze the pcap file using zeek: 

![img](https://s2.loli.net/2023/11/28/cGrzZR4JUiXnhf8.png)

The result output log files **do not include** a **dns.log** file. 

![img](https://s2.loli.net/2023/11/28/h9LWtCoGO8QKbTx.png)

Which means that the default used signature does not analyze DNS traffic. And since our challenge is to find the IP address of the DNS server, we need to build a new signature to detect and alert for DNS traffic and use it.

 

We create a new .sig file that includes the needed related info to detect DNS traffic and save it as a dns.log file later:

  

![img](https://s2.loli.net/2023/11/28/qOErw9fvAZpTbRm.png)

However, it turned out that neither any text editor (nano, vim, vi..) is installed on this shell…..

So, I returned to my kali machine, and created the signature file there:  (named it: dns_script.sig)

![img](https://s2.loli.net/2023/11/28/a2NMT74YkKLv1WF.png)

The signature file included:

Filtering for UDP protocol, filtering for port 53 UDP, and naming the event in the log file as: ‘found dns”:

![img](https://s2.loli.net/2023/11/28/my7YRAqec4SCQTO.png)

 

Now, we use zeek again to read the traffic captured file, and use the option -s to specify the signature file that we want to use:

![img](https://s2.loli.net/2023/11/28/mBl3gWQuTxHAoYk.png)

The result now has a **dns.log** file!

![img](https://s2.loli.net/2023/11/28/ke2LJGrpI8ZRN13.jpg)

We open the dns.log file, and find that the destination IP address for the dns messages (the DNS server) is: 172.16.052:

![img](https://s2.loli.net/2023/11/28/WvOXkoDaTeAI5yQ.png)

And our flag is:    <mark>falg{172.16.0.52}</mark>

***

 

Happy Practicing & Learning!

 ![Microsoft Office Signature Line...](https://s2.loli.net/2023/11/28/Vtr9RcWax5k8OIU.png)