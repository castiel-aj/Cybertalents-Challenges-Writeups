<center><b><h1>Arp Storm</h1></b></center>

***

![image-20231208183753885](https://s2.loli.net/2023/12/08/dQGDBMhbs89Pvqf.png)



\- Opening the network capture file, we find that it's only about **ARP** messages. We also notice that the only different thing among the ARP messages is the value of the **Opcode field**.

![image-20231208184327423](https://s2.loli.net/2023/12/08/rQ4xMXfTDLYbmgO.png)

to extract those values, we use the **Tshark** tool, using the command:

#**tshark -r ARP+STORM.pcap**

![image-20231208185212647](https://s2.loli.net/2023/12/08/ATqmOS6UI3W1McN.png)

to extract only the opcode values, we use the **cut** command to extract the info in the 19,20 columns to a file named encoded_flag.txt:

#**tshark -r ARP+Storm.pcap  | cut -d " " -f  19,20 > encoded_flag.txt**

![image-20231208185611779](https://s2.loli.net/2023/12/08/zfxO5LkTVFrsQIg.png)

we edit the file manually to remove the **opcode** words, and make it consistent.

Then, we extract only the last 4 digits frim the values by using the cut command again and sending the output to a new text file (encoded_opcode.txt):

#**cat encoded_flag.txt  | cut -d x -f 2 > encoded_opcode.txt**

\- Now, we take all the hex values that we have left, and transfer it to a readable text using the **XXD** tool:

#**cat encoded_opcode.txt | xxd -r -p** 

![image-20231208190254671](https://s2.loli.net/2023/12/09/ZI9PH5jSEBJU2Dc.png)

the result is: ZmxhZ3tnckB0dWl0MHVzXzBwY09kZV8xc19BbHdAeXNfQTZ1U2VkX3QwX3AwMXMwbn0=  

which is a base64 string

\- We try now to decode it from its **base64** form using **echo**:

#**echo -n "ZmxhZ3tnckB0dWl0MHVzXzBwY09kZV8xc19BbHdAeXNfQTZ1U2VkX3QwX3AwMXMwbn0=" | base64 -d**

![image-20231208190619812](https://s2.loli.net/2023/12/09/osltrgikaGPRj8Y.png)

and the flag is: **flag{gr@tuit0us_0pcOde_1s_Alw@ys_A6uSed_t0_p01s0n}**           



---



Practicing & Learning!

![Microsoft Office Signature Line...](https://s2.loli.net/2023/11/28/t28QypJLXn9lezg.png)