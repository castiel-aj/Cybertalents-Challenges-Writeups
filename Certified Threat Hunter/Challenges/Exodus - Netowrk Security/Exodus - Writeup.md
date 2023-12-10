<center><b><h1>Exodus</h1></b></center>

***



![image-20231210144647830](https://s2.loli.net/2023/12/10/TaWgDr3AS69eq8n.png)

\- After opening the file with Wireshark, I found 4 ICMP packets with a packet length of 55 bytes. So, it might be an ICMP data exfiltration.
![img1](https://s2.loli.net/2023/12/10/EuXJ3q6clhVi9On.png)

We an use **tshacrk** to get the data from the packets and save it to "output.txt" by running the following command:

 `tshark -r eXodus.pcapng -Y icmp -T fields -e data.data > output.txt`

or copy the data value from each packet as shown below

![img1 (1)](https://s2.loli.net/2023/12/10/M8l9Qra6J5bNgKz.png)

\- later in the Wireshark file, we see a file download via http that shows the **key** is "**STAR**"
select the data from each packet and paste in [cyberchef](https://github.com/vphruz/Cybertalents-Blue-Team-Writeups23/blob/main/Threat-Hunter/ex0dus/gchq.github.io) using **"from hex"** and **"XOR"** as the recipe. as shown below. when you put in the last packet and decode it, your output should end with an equal sign **("=")** which is an indicator that it's a **base64** string

[![img1 (1)](https://s2.loli.net/2023/12/10/SbEtnvLwme25AH1.png)](https://github.com/vphruz/Cybertalents-Blue-Team-Writeups23/blob/main/Threat-Hunter/ex0dus/img2.png)
put all the outputs together in **cyberchef** and convert from base64. you'll get an output that starts with "**PK**" indicating a **zip** file.
[![img1 (1)](https://s2.loli.net/2023/12/10/Hvrmc9nAx8EJsjC.png)](https://github.com/vphruz/Cybertalents-Blue-Team-Writeups23/blob/main/Threat-Hunter/ex0dus/img3.png)
save the [file](https://github.com/vphruz/Cybertalents-Blue-Team-Writeups23/blob/main/Threat-Hunter/ex0dus/download.zip) and extract it. you'll get an image with the flag in it.



\- The flag is: **FLAG{M1gratingOutOfYourNetXWOXrk}**

***



Happy Practicing & Learning!

 ![Microsoft Office Signature Line...](https://s2.loli.net/2023/11/28/t28QypJLXn9lezg.png)