<center><b><h1>WormSeen</h1></b></center>

***



![image-20231209101441873](https://s2.loli.net/2023/12/09/7FzgbLmUXT1ZfPB.png)

 The password of the zip file is: **infected**



\- After extracting the zip file with the password (infected), we find an executable file called **worm.exe**

So, our job to analysis this executable (mostly a malware) to find our flag answers.

\- I used [**Detect it Easy**](https://www.majorgeeks.com/files/details/detect_it_easy.html), which is a packer identifier for quickly defining file types and more.

![image-20231209101927656](https://s2.loli.net/2023/12/09/2Z6c9KmAqn1skIX.png)

As we can see, this file has been packed using **PyInstaller**. We need to unpack it using **[PyInstaller Extractor](https://github.com/extremecoders-re/pyinstxtractor)**.

![image-20231209102351699](https://s2.loli.net/2023/12/09/4lWU7iyfg3CEXrB.png)

Now, we can see the unpacked files, and one of them is interesting as its name is: **worm.pyc**

![Capture](https://s2.loli.net/2023/12/09/2VoL6iBWkfgMYrt.png)

Now, to see the actual python code of the **worm.pyc** file, we will use the  **[Decompyle++](https://github.com/zrax/pycdc)**.

The python script of that file is:



![image-20231209102951470](https://s2.loli.net/2023/12/09/JyuForCdk2Sj9eH.png)

![image-20231209103007810](https://s2.loli.net/2023/12/09/RiknPDH3QqFKbu6.png)

From these details we can find that the destination range is **192.168.1.0/24**, the destination port is the default SSH port **22** and the number of hosts affected is **85**.



\- The flag is: **flag{192.168.1.0/24:22:85}**

***

 

Happy Practicing & Learning!

![Microsoft Office Signature Line...](https://s2.loli.net/2023/11/27/AdW3yEBXLRlZ6pY.png)