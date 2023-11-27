 

<center><b><h1>Backdoor - Writeup</h1></b></center>

***



\- we filter the messages of the pcap file to only <font color='red'>ftp</font> messages as it is the only vulnerable protocol in among the messages

 

then, we check the first message of them (they are only 4 messages)

we can find that <mark style="background-color:grey">it is a reply message from the server to the attacker</mark>



\- from this message, we can find:

it is an <B>internal IP address</B> (the attacker address)

the <font color='green'>source IP address</font> (the attacker address)

the <font color='royalblue'>destination mac address</font> (the server address) 

then, we only need now the <font color='yellow'>CVE number</font> of the vulnerability......

from digging deep into the first ftp message, we can find that the version of the ftp used is:

<mark>220 (vsFTPd 2.3.4)\r\n</mark>

by googling this version, we find that it is vulnerable and there is a CVE number for it ...

 

the final flag is:

<mark>flag{Internal:192.168.1.58:CVE-2011-2523:08:00:27:66:e3:8b}</mark>

***



Happy Practicing & Learning!

![Microsoft Office Signature Line...](https://s2.loli.net/2023/11/27/vFafDuAoHzBnK9P.png)