<center><b><h1> Creepy DNS </h1></b></center>

***



1. open the pcap file

2) notice that there are many subdomains of Cybertalents that starts with a strange letter (ex: <font color='red'>Z</font>cybertalents, 

<font color='red'>G</font>cybertalents....) 

extract those subdomains

3) collect the first letter of each subdomain

I used <font color='green'>tshark</font> with the following filters to get them: 

 #tshark -r dns.pcapng -Y "dns" -T fields -e dns.qry.name | awk -F'[\t.]' '/cybertalents\.com/ { seen[$(NF-2)]++; if (seen[$(NF-2)] == 4) { printf "%s", $(NF-2); delete seen[$(NF-2)] } }' 

 

4) the final result is a base64 output, we should decode it to get the flag

the flag is : <mark>flag{tshArk_Is_Awes0me_Netw0rking_to0l}</mark>

***



Happy Practicing & Learning!

 ![Microsoft Office Signature Line...](https://s2.loli.net/2023/11/27/AHO6nIvJCbcVt1F.png)