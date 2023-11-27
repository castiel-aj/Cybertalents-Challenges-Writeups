<center><b><h1>Bean Detector</h1></b></center>

***



![img](https://s2.loli.net/2023/11/27/KQglXfFSWVv4Nqe.png)



\- After opening the log file, we notice that a specific IP address is fuzzing the website using the tool <font color='yellow'>Wfuzz</font> 

to get the answers of the challenge questions, we search for a <b>log</b> that has a code <b>200</b> to get the critical file

and the log is: 



<font color='red'>172.17.0.1</font> - - [<font color='purple'>12/Jun/2022:11:05:12</font> +0000] "GET /files../home/flag.txt HTTP/1.1" <mark>200</mark> <font color='blue'>49</font> "-" "Mozilla/5.0 (X11;

 Ubuntu; Linux x86_64; rv:95.0) Gecko/20100101 Firefox/95.0" "-"

 

<font color='red'>x: 172.17.0.1</font>

<font color='yellow'>y: wfuzz</font>        

<font color='blue'>z: 49</font>

<font color='purple'>w: 12/<mark style="background-color:green">06</mark>/2022:11:05:12</font>

 

<mark style="background-color:green">the flag was not accepted until we entered the month in numbers and not by its name (Jun)</mark>

flag{172.17.0.1:wfuzz:49:12/06/2022:11:05:12}

***



 

![Microsoft Office Signature Line...](https://s2.loli.net/2023/11/27/7spoTq2yYxJ8D9b.png)