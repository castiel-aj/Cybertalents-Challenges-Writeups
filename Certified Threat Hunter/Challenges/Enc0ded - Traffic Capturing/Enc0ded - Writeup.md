<center><b><h1>Enc0ded - Writeup</h1></b></center>

***



![img](https://s2.loli.net/2023/11/28/Cc2l5bLge6kwori.jpg)



 - Opening the downloaded .pcap file with Wireshark, we see that all the messages are ARP messages with the same information (source / destination, length) which are not useful to our hunt. Except for the (**opcode value**) of the ARP header which has an unknown value 

![img](https://s2.loli.net/2023/11/28/vNCawdStu2TfXxg.png)

**Note:** **ARP opcode are categorized by IANA into 3 categories:**

**1)** Assigned values (1 – 25)

**2)** Unassigned values (25 – 65534)

**3)** Reserved (65535)

And here are the assigned ones with their description: [Iana-arp-parameters](https://www.iana.org/assignments/arp-parameters/arp-parameters.xhtml)

![img](https://s2.loli.net/2023/11/28/d3sHolT2mySPfFa.jpg)

 

\- All that makes us certain that the hex values of the opcode have our flag.

To collect them, we start by dumping those ARP messages into a text file using tshark tool with the command:

 

Tshark -r ARP+Storm.pcap

<center>

![img](https://s2.loli.net/2023/11/28/vP743mIKSf8DHr2.jpg)

 

Now, in order to extract only the opcode value, we will use the **cut** command, which will let us choose which column (field) of the output to extract after specifying the diameter between the columns 

And also will redirect the output into a text file to save it

using this command:

<mark>Tshark -r ARP+Storm.pcap | cut -d -f 19,20 > encoded_flag.txt</mark>

 

![img](https://s2.loli.net/2023/11/28/DJt3jhfgLkw6xVE.jpg)

 

 

The result output in the file is:

 

![img](https://s2.loli.net/2023/11/28/TBZM659NXEfxLjC.jpg)

We need to organize it (delete the *opcode*) so we can sue the cut command again and have only the last section of the value (without the **0x**)

This is the file context when done:

![img](https://s2.loli.net/2023/11/28/vqGX3rahIjAc69U.jpg)

Now, to extract the last section of the hex (delete the **0x**) to be able to decode it into a readable text, we use the following command:

 

cat encoded_flag.txt | cut -d "x" -f 2 | xxd -r -p

![img](https://s2.loli.net/2023/11/28/rFvpTub7w8JZMd4.png)

and the result is:   ZmxhZ3tnckB0dWl0MHVzXzBwY09kZV8xc19BbHdAeXNfQTZ1U2VkX3QwX3AwMXMwbn0= 

which is a base64 encoded value. We decode:

echo -n "ZmxhZ3tnckB0dWl0MHVzXzBwY09kZV8xc19BbHdAeXNfQTZ1U2VkX3QwX3AwMXMwbn0=" | base64 -d

and have our flag: flag{gr@tuit0us_0pcOde_1s_Alw@ys_A6uSed_t0_p01s0n}  

![img](https://s2.loli.net/2023/11/28/1HYFfCbRSig9Ld4.jpg)

***



Happy Practicing & Learning!

 ![Microsoft Office Signature Line...](https://s2.loli.net/2023/11/28/t28QypJLXn9lezg.png)
