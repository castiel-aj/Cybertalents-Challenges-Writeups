<center><b><h1>Missey - Writeup</h1></b></center>

***



![img](https://s2.loli.net/2023/11/28/JsTydac72kHAL5m.jpg)



\- Since we’re told that there were a bruteforce attack, once we open the capture file, we check the statistics of the conversations to find which IP address had the most conversations number:

![img](https://s2.loli.net/2023/11/28/qAxCm2hvun98zcE.png)

We notice that the source IP “192.168.1.7” has sent many messages to the range “192.126.117.0” **(was bruteforcing the subnet)**

![img](https://s2.loli.net/2023/11/28/laEUxKudipBjtQf.png)

By starting to dig inside each of these packets, we notice that the most notable different among them is the hex value of their payload. So, we extract these values using tshark: 

 

tshark -r Missey.pcap -e "tcp.payload" -T fields -Y "ip.src==192.168.1.7 and ip.dst==192.126.117.0/24"

where we specified the file using **-r,** specified the field we want to extract using **-e**, the output format to be in a tabular format with fields separated by delimiters using **-T**, and to apply a filter using the **-Y** option



![img](https://s2.loli.net/2023/11/28/xGAqrDbm38lfipe.jpg)

Now, we use the ‘**XXD**” tool to reverse the hexadecimal representation of the output data into binary form (**-r** for reverse, **-p** for plain hexdump)

tshark -r Missey.pcap -e "tcp.payload" -T fields -Y "ip.src==192.168.1.7 and ip.dst==192.126.117.0/24" | xxd -r -p  

 

![img](https://s2.loli.net/2023/11/28/6lXYFZrf5gEwJpV.png)

 

we try to find any flag in it using grep, but fail ….

 

So, we use the **XXD** command again, and grep for the word “**FLAG**”

tshark -r Missey.pcap -e "tcp.payload" -T fields -Y "ip.src==192.168.1.7 and ip.dst==192.126.117.0/24" | xxd -r -p |xxd -r -p | grep FLAG

![img](https://s2.loli.net/2023/11/28/P6AStROLyYoIarx.png)

 and the flag is     FLAG{M15SED_INBY73$}  . However, it did not work until we deleted the “3” from it…

and the final accepted flag is:    <mark>FLAG{M15SED_INBY7$} </mark>

***



Happy Practicing & Learning!

 ![Microsoft Office Signature Line...](https://s2.loli.net/2023/11/28/dIpkTqZsXwW4aiV.png)
