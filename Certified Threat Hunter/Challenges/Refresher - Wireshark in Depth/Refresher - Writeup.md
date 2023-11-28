<center><b><h1>Refresher - Writeup</h1></b></center>

***



![img](https://s2.loli.net/2023/11/28/UqVW2CczeghGKJl.jpg)

 

\- I started analyzing the .pcap file on windows using **Wireshark**, the file has a lot of messages and checking them individually is not logical. So, I decided to check the most used protocols in this file:

Statistics ---------------------- Protocol Hierarchy

![img](https://s2.loli.net/2023/11/28/LpDO4inN7I5h8zH.png)

And the result was:

![img](https://s2.loli.net/2023/11/28/snRXdbW8gIa7mHT.jpg)



Clearly, many TCP messages, and few HTTP, FTP ones.

I started digging into the FTP messages because it has high possibility of giving us a lead like **(**credentials, downloaded files, failed authentication…..**)**

I applied a **filter** for the FTP messages, and then **followed** up their **TCP stream**:

![img](https://s2.loli.net/2023/11/28/WGZl8kmrvHhX9A6.jpg)

![img](https://s2.loli.net/2023/11/28/8UrfvnmCcTHstQM.jpg)



When analyzing the TCP stream of the FTP connection, I noticed that the user had a successful login, then downloaded an archive named **secret.zip** (this means that we’re going in the right way and found our first lead 😊)

![img](https://s2.loli.net/2023/11/28/fWx6BLM8csezSOH.jpg)

In order to download this archive, we try to find its message in this stream by scrolling to the next messages of the flow:

and as shown below, when I found the message it was clear that the archive has the **flag.txt** file !

![img](https://s2.loli.net/2023/11/28/OwZK3sUaeFbGjT8.png)

 

to save the archive, we made the data in a **row** format, and chose to save it as a secret.zip file:

![img](https://s2.loli.net/2023/11/28/GPfLXpW4jSdNbAD.png)

The secret.zip file had a password unfortunately! And when I tried to crack it using **JohnTheRipper**, it took ages in cracking it….

So, I decided to go back to the capture file, and search in the HTTP stream so maybe find something helpful…

When I filtered for the HTTP protocol, I noticed that it had many downloads for images!

So, I decided to export these messages and check them:

 

![img](https://s2.loli.net/2023/11/28/IqtDmUOjKzEebNC.jpg)

And save them all:

![img](https://s2.loli.net/2023/11/28/OR2NnXLxiVozTw4.png)

Some of the exported images were **named in a sequential pattern** and with **one letter**, and by focusing on their names, I noticed that combining all their names would **form a meaningful sentence**:

 

![img](https://s2.loli.net/2023/11/28/FmAopTcfySz7b8h.png)

Extracting the key letters from the images names could be done using “cut command” many times, or by only writing them one by one…

The result would be the same:  **iamsupersecretpasswordgood4uthefinding**

I used the extracted word to open the secret.zip file and It worked!

The archive had only one file named flag.txt and had our falg : **flag{y0u_c0m3_f0r_fl1g_1nd_h3r3_1t_1s_2000}**



![img](https://s2.loli.net/2023/11/28/ARovH8BkaFwN6pz.png)

***

 Happy Practicing & Learning!

 ![Microsoft Office Signature Line...](https://s2.loli.net/2023/11/28/dIpkTqZsXwW4aiV.png)
